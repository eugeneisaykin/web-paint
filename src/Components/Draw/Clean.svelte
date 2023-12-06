<script>
	/**
	 * Svelte
	 */
	import { getContext } from 'svelte';
	import MdDelete from 'svelte-icons/md/MdDelete.svelte'

	/**
	 * GetContext
	 */
	const isClean = getContext("isClean");
</script>

<button
	on:click={() => {
		$isClean = !$isClean
	}}
>
	<MdDelete/>
</button>

<style lang="scss">
	button {
		cursor: pointer;
		width: 36px;
		height: 36px;
	}
</style>