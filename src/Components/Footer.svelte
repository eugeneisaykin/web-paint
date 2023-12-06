<script>
	import Palette from './Colors/Palette.svelte'
	import ColorSelection from './Colors/ColorSelection.svelte'
</script>

<div class="footer">
	<Palette />
	<ColorSelection />
</div>


<style lang="scss">	
	.footer {
		display: flex;
		justify-content: space-between;
	}
</style>