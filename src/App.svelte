<script>
	let path = '';
	
	let min = -10;
	let max = 10;

	let scale = 1;
	let xOffset = 0;
	let yOffset = 0;

	$: {
		path = '';
		for (let i = min; i <= max; i++) {
			let x = i;
			let y = x*x;

			// scale
			x = x*scale;
			y = y*scale;

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

<label for="scale">scale</label>
<input id="scale" type="range" bind:value={scale} min={min} max={max}>

<label for="xOffset">xOffset</label>
<input id="xOffset" type="range" bind:value={xOffset} min={min} max={max}>

<label for="yOffset">yOffset</label>
<input id="yOffset" type="range" bind:value={yOffset} min={min} max={max}>

<div class="graph-container">
	<svg viewBox="{min} {min} {max*2} {max*2}" class="graph">
		<path d={path} fill="green" />
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
</style>