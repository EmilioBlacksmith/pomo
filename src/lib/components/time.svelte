<script lang="ts">
	let { time = 0 } = $props();

	let minutes = $derived(Math.floor(time / 60));
	let seconds = $derived(time % 60);

	let formattedSeconds = $derived(seconds.toString().padStart(2, '0'));
</script>

<div class="absolute flex flex-col items-center justify-center gap-1">
	<h1 class="font-mono text-5xl">
		{minutes}:{formattedSeconds}
	</h1>
</div>
