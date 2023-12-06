<script>
	/**
	 * Svelte
	 */
	import { getContext } from 'svelte';
	import { fade } from 'svelte/transition';
	/**
	 * GetContext
	 */
	const isRoulette = getContext("isRoulette");
</script>

<button on:click={() => $isRoulette = !$isRoulette}
	class:active={$isRoulette}>
	<img src="/public/svg/ruler.svg" alt="">
</button>

<style lang="scss">
	button {
		width: 36px;
		height: 36px;
		// position: relative;
		img {
			width: 15px;
			height: 15px;
		}
		&.active {
			background-color: gray;
		}
	}
	
</style>
