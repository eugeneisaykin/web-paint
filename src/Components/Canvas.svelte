<script>
	/**
	 * Svelte
	 */
  import { onMount, getContext } from 'svelte';
	/**
	 * Props
	 */
  export let width = 700;
  export let height = 700;
  const background = '#fff';
  
	/**
	 * GetContext
	 */
  const isErasing = getContext("isErasing");
  const isPencil = getContext("isPencil");
  const isRoulette = getContext("isRoulette");
	const {mainColor, minorColor, isFill} = getContext("color");
  const { thickness, isLine, isRectangle, isCircle, isTriangle, isFigure } = getContext("figure")
  const isSave = getContext("isSave");
  const isClean = getContext("isClean");

  let canvas;
  let context;
  let isDrawing;
  let start;
  let isRightClick;
  let imageData;
  let rouletteDist;

  let isResizing = false;
  let resizeStart;

  let t, l;

  onMount(() => {
    context = canvas.getContext('2d');
    context.lineWidth = 3;

    handleSize();
  });

  const handleStart = (event) => {
    const { offsetX: x, offsetY: y, button: btn } = event;
    
    isRightClick = btn == 2;
    context.lineWidth = $thickness;
    if($isLine || $isRectangle || $isCircle || $isTriangle || $isRoulette) {
      imageData = context.getImageData(0, 0, canvas.width, canvas.height);
    }
    isDrawing = true;
    start = { x, y };

    if (x >= width - 15 && y >= height - 15) {
      isResizing = true;
      resizeStart = { x, y };
    }
  };

  const handleEnd = () => {
    isDrawing = false;
    isResizing = false;
    if ($isRoulette) context.putImageData(imageData, 0, 0);
    
    if ($isLine || $isRoulette) {
      handleLineEnd();
    }
  };

  const cleanCanvas = () => {
    context.clearRect(0, 0, width, height);
    $isClean = false;
  }

  const saveCanvasImage = () => {
  const dataUrl = canvas.toDataURL();
  
  const link = document.createElement('a');
  link.href = dataUrl;
  link.download = 'my_drawing.png';
  link.click();
};

  const handleDrawMove = ({ offsetX: x1, offsetY: y1 }) => {
    if (!isDrawing) return;
    
    const { x, y } = start;
    context.beginPath();
    context.lineWidth = $thickness;
    if (isResizing) {
      const deltaX = x1 - resizeStart.x;
      const deltaY = y1 - resizeStart.y;
      width += deltaX;
      height += deltaY;
      resizeStart = { x: x1, y: y1 };
      handleSize();
    } else if ($isPencil) {
      context.moveTo(x, y);
      context.lineTo(x1, y1);
      context.closePath();
      context.stroke();
    } else if ($isErasing) {
      context.globalCompositeOperation = 'destination-out';
      context.arc(x1, y1, 10, 0, Math.PI * 2);
      context.fill();
      context.globalCompositeOperation = 'source-over';
    }
    start = { x: x1, y: y1 };
  };

  const handleLineEnd = () => {
    if (isDrawing && $isLine || isDrawing && $isRoulette) {
      isDrawing = false;
      context.beginPath();
      context.moveTo(start.x, start.y);
      context.lineTo(start.x1, start.y1);
      context.stroke();
    }
  };

  const handleFigureMove = ({ offsetX: x1, offsetY: y1 }) => {
    if (isResizing) {
      const deltaX = x1 - resizeStart.x;
      const deltaY = y1 - resizeStart.y;
      width += deltaX;
      height += deltaY;
      resizeStart = { x: x1, y: y1 };
      handleSize();
    } else if (isDrawing && $isLine || isDrawing && $isRoulette) {
      context.clearRect(0, 0, width, height);
      context.putImageData(imageData, 0, 0);
      if($isRoulette) {
        context.strokeStyle = "red"
      } else {
        context.strokeStyle = $mainColor;
      }
      context.beginPath();
      context.moveTo(start.x, start.y);
      context.lineTo(x1, y1);
      rouletteDist = Math.sqrt(Math.pow(x1 - start.x, 2) + Math.pow(y1 - start.y, 2));
      context.stroke();
      start = { x: start.x, y: start.y, x1, y1 };
    } else if (isDrawing && $isTriangle) {
      context.clearRect(0, 0, width, height);
      context.putImageData(imageData, 0, 0);
      context.beginPath();
      context.moveTo(start.x, start.y);
      context.lineTo(x1, y1);
      context.lineTo(x1 + start.x, y1)
      context.lineTo(start.x, start.y)
      context.stroke();
      if($isFill) {
        context.fillStyle = $minorColor;
        context.fill();
      }
      start = { x: start.x, y: start.y, x1, y1 };
    } else if (isDrawing && $isRectangle) {
      context.clearRect(0, 0, width, height);
      context.putImageData(imageData, 0, 0);
      context.strokeRect(start.x, start.y, x1 - start.x, y1 - start.y);
      if($isFill) {
        context.fillStyle = $minorColor;
        context.fillRect(start.x, start.y, x1 - start.x, y1 - start.y);
      }
    } else if (isDrawing && $isCircle) {
      context.clearRect(0, 0, width, height);
      context.putImageData(imageData, 0, 0);
      const { x, y } = start;
      const radius = Math.sqrt(Math.pow(x1 - x, 2) + Math.pow(y1 - y, 2));
      context.beginPath();
      context.arc(x, y, radius, 0, Math.PI * 2);
      context.stroke();
      if($isFill) {
        context.fillStyle = $minorColor;
        context.fill();
      }
    }
  };

  const handleSize = () => {
    const { top, left } = canvas.getBoundingClientRect();
    t = top;
    l = left;
  };

	/**
	 * Reactive
	 */

  $: if($isSave) saveCanvasImage();
  $: if($isClean) cleanCanvas();
  $: if (context || isRightClick) {
    context.strokeStyle = isRightClick ? $minorColor : $mainColor;
  }
  $: if(!$isCircle && !$isRectangle && !$isTriangle && !$isLine) $isFigure = false;
</script>

<svelte:window on:resize={handleSize} />


<div class="canvas">
  {#if $isRoulette && rouletteDist}
    <div class="dist">{rouletteDist.toFixed(2)} px</div>
  {/if}
  <canvas
  {width}
  {height}
  style:background
  bind:this={canvas}
  on:mousedown={handleStart}
	on:touchstart={e => {
		const { clientX, clientY } = e.touches[0]
		handleStart({
			offsetX: clientX - l,
			offsetY: clientY - t
		})
	}}	
  on:mouseup={handleEnd}
  on:touchend={handleEnd}
  on:mouseleave={handleEnd}
  on:mousemove={$isFigure || $isRoulette ? handleFigureMove : handleDrawMove}
  on:touchmove={$isFigure || $isRoulette ? handleFigureMove : handleDrawMove}
  on:contextmenu={event => { event.preventDefault(); }}
/>
<div class="triangle-icon">
  ▲
</div>
</div>

<style>
  .dist {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }
  .canvas {
    position: relative;
  }
  .triangle-icon {
    position: absolute;
    rotate: 130deg;
    bottom: -5px;
    right: 0px;
    width: 30px;
    height: 30px;
    cursor: pointer;
    pointer-events: none;
  }
</style>