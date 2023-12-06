<script>
	/**
	 * Svelte
	 */
	import { getContext } from "svelte";
	import MdSwapHoriz from 'svelte-icons/md/MdSwapHoriz.svelte';

	/**
	 * GetContext
	 */
	const {mainColor, minorColor, isMinorColor} = getContext("color");
</script>

<div class="color-section">
	<div class="color">
		<button on:click={() => $isMinorColor = false}>
			<svg style:color={$mainColor} viewBox="-50 -50 100 100">
				<g fill="currentColor" stroke="currentColor" stroke-width="0" stroke-linecap="round">
					<path d="M -38 12 a 38 38 0 0 0 76 0 q 0 -28 -38 -62 -38 34 -38 62" />
				</g>
			</svg>
		</button>
		<div class="title">First Color</div>
	</div>
	<div class="color">
		<button on:click={() => {[$mainColor, $minorColor] = [$minorColor, $mainColor]}}>
			<MdSwapHoriz/>
		</button>
		<div class="title">Swap</div>
	</div>
	<div class="color">
		<button on:click={() => $isMinorColor = true}>
			<svg style:color={$minorColor} viewBox="-50 -50 100 100">
				<g fill="currentColor" stroke="currentColor" stroke-width="0" stroke-linecap="round">
					<path d="M -38 12 a 38 38 0 0 0 76 0 q 0 -28 -38 -62 -38 34 -38 62" />
				</g>
			</svg>
			<div class="title">Second Color</div>
		</button>
	</div>
</div>

<style lang="scss">
	.color-section {
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

		.title {
			pointer-events: none;
			width: 100px;
			color: #FAFAFA;
			font-size: 14px;
			font-weight: 600;
			text-align: center;
			position: absolute;
			background-color: #232323;
			margin-top: 20px;
			margin-left: -40px;
			border-radius: 5px;
			padding: 5px;
			transition: opacity 0.3s ease;
			opacity: 0;
		}
		
		.color:hover .title {
			opacity: 1;
		}
	}
</style>