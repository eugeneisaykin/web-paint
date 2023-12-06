<script>
	/**
	 * Svelte
	 */
	import { getContext } from 'svelte';
	import MdSave from 'svelte-icons/md/MdSave.svelte'	
	/**
	 * GetContext
	 */
	const isSave = getContext("isSave")

</script>

<button

	on:click={() => {
		$isSave = !$isSave
	}}
>
	<MdSave/>
</button>

<style lang="scss">
	button {
		cursor: pointer;
		width: 36px;
		height: 36px;
	}
</style>