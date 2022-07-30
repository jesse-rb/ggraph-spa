<script>
	let path = '';
	
	let min = -20;
	let max = 20;

	let xScale = 0.5;
	let yScale = 0.1;

	let xOffset = 0;
	let yOffset = 0;

	$: {
		path = '';
		for (let i = min; i <= max; i++) {
			// Setup initial x = y^2
			let x = i;
			let y = x*x;

			// Scale
			x = x*xScale;
			y = y*yScale;

			// Offset
			x = x-(-1*xOffset);
			y = y-(-1*yOffset);

			path += (i==min ? 'M' : 'L')+x+' '+(-y)+ ' ';
		}
		path += 'Z';
	}

	function range(n, m) {
		let arr = [];
		for (let i = n; i <= m; i++) {
			arr.push(i);
		}
		return arr;
	}
</script>

<label for="xScale">xScale</label>
<input id="xScale" type="range" bind:value={xScale} step="0.01" min={min} max={max}>

<label for="yScale">yScale</label>
<input id="yScale" type="range" bind:value={yScale} step="0.01" min={min} max={max}>

<label for="xOffset">xOffset</label>
<input id="xOffset" type="range" bind:value={xOffset} min={min} max={max}>

<label for="yOffset">yOffset</label>
<input id="yOffset" type="range" bind:value={yOffset} min={min} max={max}>

<div class="graph-container">
	<svg viewBox="{min} {min} {max*2} {max*2}" class="graph">
		<!--The plot-->
		<path d={path} fill="green" stroke="white" stroke-width="0.2%" />
		<circle cx={xOffset} cy={-yOffset} r="1%" fill="white" />
		<!--center dot-->
		<circle cx="0" cy="0" r="1%" fill="red" />
		<!--ranges-->
		{#each range(min, max) as i}
			<text x="{i}" y="0" fill="orange" class="small">{i}</text> <!--x-->
			<text x="0" y="{i}" fill="orange" class="small">{-i}</text> <!--y-->
		{/each}
	</svg>
</div>

<style>
	.graph-container {
		width: 500px;
		height: 500px;
	}
	.graph {
		display: block;
		background-color: #2e2e2e;
		width: 100%;
		height: 100%;
	}
	.graph .small {
		font-size: 0.5px;
	}
	.graph .small:hover {
		font-size: 2px;
	}
</style>