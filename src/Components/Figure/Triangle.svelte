<script>
	/**
	 * Svelte
	 */
	import Palette from "../Colors/Palette.svelte";
	import MdFormatColorFill from 'svelte-icons/md/MdFormatColorFill.svelte'
	import { getContext } from 'svelte';
	
	/**
	 * GetContext
	 */
	const isRoulette = getContext("isRoulette")
	const isErasing = getContext("isErasing");
	const isPencil = getContext("isPencil");
	const { isFill } = getContext("color");
	const {thickness, isLine, isCircle, isRectangle, isTriangle, isFigure} = getContext("figure");

	let isPopupOpenThickness = false;
	let isPopupOpenFill = false;

	/**
	 * Reactive
	 */
	$: if($isErasing || $isPencil || $isCircle || $isRectangle || $isLine) {
		$isTriangle = false;
	} else {
		$isFigure = true;
	}

</script>

<div class="btn">
	<button
	on:mouseenter={() => (isPopupOpenThickness = true)}
	on:mouseleave={() => (isPopupOpenThickness = false)}
	class:active={$isTriangle}
	on:click={() => {
		if(!$isRoulette) {
			$isFigure = !$isFigure; 
			$isTriangle = !$isTriangle;
		}
		$isRoulette = false;
	}}
>
<span class="line-main"></span>
	{#if isPopupOpenThickness}
		<div class="popup">
			{#each [1, 2, 3, 4] as item}
				<button on:click={(event) => {
					event.stopPropagation();
					$isTriangle = true;
					isPopupOpenThickness = false;
					$thickness = item;
				}}>
					<span class="line" style="border-bottom: {item}px solid black;"></span>
				</button>
			{/each}
		</div>
	{/if}
</button>
</div>
<div class="btn">
	{#if $isTriangle}
	<button
		on:mouseenter={() => (isPopupOpenFill = true)}
		on:mouseleave={() => (isPopupOpenFill = false)}
		class="palette-main"
		class:active={$isFill}
		on:click={() => $isFill = !$isFill}
	>
	<MdFormatColorFill />
		{#if isPopupOpenFill && $isFill}
		<div class="paletter" on:click={(event) => event.stopPropagation()}>
			<Palette 
				property={"fill"}
			/>
		</div>
		{/if}
	</button>
{/if}
</div>

<style lang="scss">
	span.line-main {
		display: block;
    border-left: 10px solid transparent;
    border-right: 10px solid transparent;
    border-bottom: 15px solid black;
	}

	button {
		cursor: pointer;
		width: 36px;
		height: 36px;
		position: relative;
			span .line-main {
			border-top: 3px solid black;
		}
		.popup {
			position: absolute;
			width: 40px;
			top: 100%;
			left: -8px;
			display: flex;
			align-items: center;
			flex-direction: column;
			background-color: #fff;
			box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
			border-radius: 4px;
			padding: 4px;
			z-index: 1;
		}

		.popup button {
			cursor: pointer;
			padding: 8px;
			border: none;
			background: none;
			text-align: left;
			display: flex;
			align-items: center;
		}

		.popup .line {
			width: 20px;
		}

		&.active {
			background-color: gray;
		}
		.palette-main {
			position: relative;
		}
		.paletter {
			position: absolute;
			top: 100%;
		}
	}

</style>
