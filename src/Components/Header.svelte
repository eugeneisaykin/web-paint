<script>
	import Circle from "./Figure/Circle.svelte";
	import Eraser from './Draw/Eraser.svelte'
	import Line from './Figure/Line.svelte'
	import Pencil from './Draw/Pencil.svelte'
	import Rectangle from './Figure/Rectangle.svelte'
	import Triangle from "./Figure/Triangle.svelte";
	import Save from "./Save.svelte";
	import Clean from "./Draw/Clean.svelte";
	import Roulette from "./Roulette.svelte";
</script>

<div class="header">
	<div class="figure">
		<Rectangle />
		<Circle />
		<Triangle />
		<Line />
	</div>
  <div class="draw">
		<Roulette />
		<Save />
		<Pencil />
		<Eraser />
		<Clean />
	</div>
</div>


<style lang="scss">	
	.header {
		display: flex;
		justify-content: space-between;
		.figure, .draw {
			display: flex;
			gap: 3px;
			margin-bottom: 3px;
		}
		.draw {
			display: flex;
			margin-bottom: 3px;
			gap: 7px;
		}
	}
</style>