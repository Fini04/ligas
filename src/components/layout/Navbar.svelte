<script lang="ts">
	import Timer from '@components/elements/Timer.svelte';
	import { TimerState } from '@lib/timer';
	import activeSession from '@stores/activeSession';
	import {
		MenuIcon,
		PauseIcon,
		PlayIcon,
		RotateCcwIcon,
	} from 'svelte-feather-icons';
	import { _ } from '@lib/util/translations';

	const pauseTimer = () => activeSession.updateSelf(x => x.timer.pause());
	const resetTimer = () =>
		activeSession.updateSelf(x => {
			if (confirm($_('timer.reset_prompt'))) x.timer.reset();
		});
</script>

<nav class="navbar sticky top-0 z-50 bg-base-300 text-3xl text-justify">
	<!-- navbar content -->
	<div class="navbar-start">
		<label for="drawer-toggle" class="btn btn-ghost btn-square lg:hidden">
			<MenuIcon />
		</label>
	</div>

	<h1 class="navbar-center h-12 hidden md:flex">LIGAS</h1>

	<div class="navbar-end">
		<button on:click={pauseTimer} class="btn btn-ghost btn-square">
			{#if $activeSession.timer.state === TimerState.Running}
				<PauseIcon />
			{:else}
				<PlayIcon />
			{/if}
		</button>
		<p class="px-2 h-12">
			<Timer />
		</p>
		<button on:click={resetTimer} class="btn btn-ghost btn-square">
			<RotateCcwIcon />
		</button>
	</div>
</nav>
