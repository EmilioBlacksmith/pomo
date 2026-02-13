<script>
	export let progress = 100;

	$: offset = 100 - progress;
</script>

<svg width="300" height="300" viewBox="0 0 130 130" style="transform: rotate(-90deg);">
	<circle cx="65" cy="65" r="61.5" fill="none" stroke="#008537" stroke-width="10" />

	<circle
		cx="65"
		cy="65"
		r="61.5"
		fill="none"
		stroke="lightgreen"
		stroke-width="10"
		pathLength="100"
		stroke-dasharray="100"
		stroke-dashoffset={offset}
		style="transition: stroke-dashoffset 1s linear;"
	/>
</svg>
