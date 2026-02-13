<script lang="ts">
	import { onDestroy } from 'svelte';
	import Logo from '$lib/components/logo.svelte';
	import Circle from '$lib/components/circle.svelte';
	import Time from '$lib/components/time.svelte';

	let isActive = $state(false);
	let isPaused = $state(false);
	let countdown = $state(25 * 60);
	let interval: any;

	function startTimer() {
		isActive = true;
		isPaused = false;
		runInterval();
	}

	function resumeTimer() {
		isPaused = false;
		runInterval();
	}

	function pauseTimer() {
		isPaused = true;
		clearInterval(interval);
	}

	function runInterval() {
		clearInterval(interval);
		interval = setInterval(() => {
			if (countdown > 0) {
				countdown -= 1;
			} else {
				finish();
			}
		}, 1000);
	}

	function finish() {
		clearInterval(interval);
		isActive = false;
		isPaused = false;
		countdown = 25 * 60;
	}

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<main
	class="flex min-h-screen w-screen flex-col items-center justify-center bg-emerald-950 text-lime-200"
>
	<Circle progress={1} />

	{#if isActive}
		<Time time={countdown} />

		<div class="z-10 mt-8 flex gap-4">
			{#if isPaused}
				<button
					onclick={resumeTimer}
					class="cursor-pointer rounded-full bg-lime-600 px-6 py-2 font-bold text-white transition hover:bg-lime-500"
				>
					Resume
				</button>
			{:else}
				<button
					onclick={pauseTimer}
					class="cursor-pointer rounded-full border border-emerald-600 bg-emerald-800/50 px-6 py-2 text-lime-200 transition hover:bg-emerald-800"
				>
					Pause
				</button>
			{/if}

			<button
				onclick={finish}
				class="cursor-pointer rounded-full px-4 py-2 text-emerald-500 transition hover:text-emerald-300"
			>
				Cancel
			</button>
		</div>
	{/if}

	{#if !isActive}
		<Logo />
		<button
			onclick={startTimer}
			class="mt-4 cursor-pointer rounded-full bg-emerald-800 px-4 py-2 text-white transition hover:bg-emerald-700"
		>
			Start 25 min focus
		</button>
	{/if}
</main>
