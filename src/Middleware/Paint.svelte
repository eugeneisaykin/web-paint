<script>
	/**
	 * Svelte
	 */
	import { setContext } from "svelte";
	import { writable } from "svelte/store";


	/**
	 * Store
	 */
	const 
		isPencil = writable(true),
		isErasing = writable(false),
		isLine = writable(false),
		isRectangle = writable(false),
		isTriangle = writable(false),
		isCircle = writable(false),
		isFigure = writable(false),
		thickness = writable(3),
		mainColor = writable("#000"),
		minorColor = writable("#FFF"),
		isMinorColor = writable(false),
		isSave = writable(false),
		isClean = writable(false),
		isRoulette = writable(false),
		isDraw = writable(false),
		isFill = writable(false);

	/**
	 * Set Context
	*/
	setContext("isPencil", isPencil);
	setContext("isSave", isSave);
	setContext("isClean", isClean);
	setContext("isErasing", isErasing);
	setContext("isDraw", isDraw);
	setContext("isRoulette", isRoulette)
	setContext("figure", {
		isFigure,
		isLine,
		isRectangle,
		isTriangle,
		isCircle,
		thickness,
	})
	setContext("color", {
		mainColor,
		minorColor,
		isMinorColor,
		isFill,
	})
</script>

<slot />
