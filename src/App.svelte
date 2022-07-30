<script>
	let path = '';
	let slider = 1;
	let min = -10;
	let max = 10;
	$: {
		path = '';
		for (let i = min; i <= max; i++) {
			let x = i;
			let y = x*x;

			// scale
			x = x*slider
			y = y*slider

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

<input type="range" bind:value={slider} min="-100" max="100">

<div class="graph-container">
	<svg viewBox="{min} {min*max} {max*2} {max*max*2}" class="graph">
		<path d={path} fill="green" />
		<circle cx="0" cy="0" r="1%" fill="red" />
		{#each range(min, max*2) as i}
			<text x="{i*max}" y="10" fill="orange" class="small">{i}</text>
			<text x="5" y="{i*max}" fill="orange" class="small">{-i}</text>
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
		font-size: 5px;
	}
</style>