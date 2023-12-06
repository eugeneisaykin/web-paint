<script>
	/**
	 * Svelte
	 */
	import { getContext } from 'svelte';
	import FaEraser from 'svelte-icons/fa/FaEraser.svelte';
	
	/**
	 * GetContext
	 */
	const isErasing = getContext("isErasing");
	const isPencil = getContext("isPencil");
	const { isFigure } = getContext("figure");
	const isRoulette = getContext("isRoulette");
	
	/**
	 * Reactive
	 */
	$: if($isFigure || $isPencil) $isErasing = false; 
</script>

<button
	class:active={$isErasing}
	on:click={() => {
		if(!$isRoulette) $isErasing = !$isErasing;
		$isRoulette = false;
	}}
>
	<FaEraser/>
</button>

<style lang="scss">
	button {
		cursor: pointer;
		width: 36px;
		height: 36px;
		
		&.active {
			background-color: gray;
		}
	}
</style>