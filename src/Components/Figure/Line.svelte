<script>
	/**
	 * Svelte
	 */
	import { getContext } from 'svelte';
	import { fade } from 'svelte/transition';

	/**
	 * GetContext
	 */
	const isErasing = getContext("isErasing");
	const isPencil = getContext("isPencil");
	const {thickness, isLine, isCircle, isRectangle, isTriangle, isFigure} = getContext("figure");

	let isPopupOpen = false;

	/**
	 * Reactive
	 */
	$: if($isErasing || $isPencil || $isCircle || $isRectangle || $isTriangle) {
		$isLine = false; 
	} else {
		$isFigure = true;
	}
</script>

<div class="btn">
	<button
	on:mouseenter={() => (isPopupOpen = true)}
	on:mouseleave={() => (isPopupOpen = false)}
	class:active={$isLine}
	on:click={() => {
		$isLine = !$isLine;
		$isFigure = !$isFigure;
	}}
>
<span class="line-main"></span>
	{#if isPopupOpen}
		<div class="popup" transition:fade>
			{#each [1, 2, 3, 4] as item}
				<button on:click={(event) => {
					event.stopPropagation();
					$isLine = true;
					isPopupOpen = false;
					$thickness = item;
				}}>
					<span class="line" style="border-bottom: {item}px solid black;"></span>
				</button>
			{/each}
		</div>
	{/if}
</button>
</div>

<style lang="scss">
	span.line-main {
		display: block;
		border-top: 3px solid black;
		transform: rotate(45deg);
		transform-origin: 50% 50%;
	}

	button {
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
	}
</style>
