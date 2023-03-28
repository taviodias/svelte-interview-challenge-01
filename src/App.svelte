<script>
  let points = [];
  let popedPoints = [];

  function handleClick(event) {
    if(popedPoints.length > 0)
      popedPoints = [];
    points = [...points, {X: event.clientX, Y: event.clientY}];
    console.log('Point')
    console.log({points});
    console.log({popedPoints});
  }

  function handleUndo(event) {
    event.stopPropagation();
    if(points.length === 0) return;
    console.log('Undo');
    popedPoints.push(points.pop());
    points = points;
    console.log({points});
    console.log({popedPoints});
  }

  function handleRedo(event) {
    event.stopPropagation();
    if(popedPoints.length === 0) return;
    console.log('Redo');
    points = [...points, popedPoints.pop()];
    console.log({points});
    console.log({popedPoints});
  }
</script>

<div class="h-screen w-full bg-slate-700 relative" on:click={handleClick}>
  <div class="fixed top-2 left-1/2 -translate-x-1/2 flex gap-1">
    <button class="bg-slate-200 px-4 py-1 hover:bg-slate-300" on:click={handleUndo}>Undo</button>
    <button class="bg-slate-200 px-4 py-1 hover:bg-slate-300" on:click={handleRedo}>Redo</button>
  </div>
    {#each points as point}
      <span class="absolute h-2 w-2 bg-red-500 rounded -translate-x-1/2 -translate-y-1/2" 
        style="left: {point.X}px; top: {point.Y}px" 
      />
    {/each}
</div>
