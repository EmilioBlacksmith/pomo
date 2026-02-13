<script lang="ts">
	import Time from './time.svelte';
	import type { Snippet } from 'svelte';

	let { progress = 1, countdown = 0, isActive = false, children }: { progress?: number; countdown?: number; isActive?: boolean; children?: Snippet } = $props();

	let offset = $derived(100 - progress * 100);
</script>

<div class="relative inline-flex items-center justify-center">
	<svg width="400" height="400" viewBox="0 0 130 130" class="-rotate-90">
		<circle cx="65" cy="65" r="61.5" fill="none" stroke="#064e3b" stroke-width="6" />

		<circle
			cx="65"
			cy="65"
			r="61.5"
			fill="none"
			stroke="#008537"
			stroke-width="6"
			stroke-linecap="round"
			pathLength="100"
			stroke-dasharray="100"
			stroke-dashoffset={offset}
			style="transition: stroke-dashoffset 1s linear;"
		/>
	</svg>

	<div class="absolute inset-0 flex flex-col items-center justify-center">
		{#if isActive}
			<Time time={countdown} />
		{:else if children}
			{@render children()}
		{/if}
	</div>
</div>
