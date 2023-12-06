<script>
	/**
	 * Svelte
	 */
	import { getContext } from "svelte";
	
	/**
	 * GetContext
	 */
	const {mainColor, minorColor, isMinorColor} = getContext("color");

	/**
	 * Props
	 */
	export let property = false;

	const colors = [
		'#000000',
		'#ffffff',
		'#d58141',
		'#d7c44c',
		'#4fa9cc',
		'#3f8d27',
	]
</script>

<div class="palette">
	{#each colors as color}
		<button 
			on:click="{() => {
				if($isMinorColor || property) {
					$minorColor = color;
					} else {
					$mainColor = color;
				}
			}}"
			style:background={color}>
		</button>
	{/each}
</div>

<style lang="scss">
	.palette {
		margin-top: 10px;
		display: flex;
		align-items: center;
		gap: 10px;
		
			button  {
			width: 36px;
			height: 36px;
			cursor: pointer;
			margin: 0;
			svg {
				width: 16px;
				height: 16px;
			}
		}
	}
</style>