<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	export let index: number = 0;
	export let percent: number = 0;
	export let indexStarHover: number | undefined = undefined;

	const dispatch = createEventDispatcher();

	const onMouseEnter = () => {
		dispatch('hover', index);
	};

	const onClickStar = () => dispatch('click', index + 1);
</script>

<div
	class="stars"
	on:mouseenter={onMouseEnter}
	role="button"
	tabindex="0"
	on:mousedown={onClickStar}
>
	<svg viewBox="0 0 534.765 512.736" xmlns="http://www.w3.org/2000/svg">
		<path
			d="M 237.946 18.536 L 172.646 150.936 L 26.546 172.236 C 0.346 176.036 -10.154 208.336 8.846 226.836 L 114.546 329.836 L 89.546 475.336 C 85.046 501.636 112.746 521.336 135.946 509.036 L 266.646 440.336 L 397.346 509.036 C 420.546 521.236 448.246 501.636 443.746 475.336 L 418.746 329.836 L 524.446 226.836 C 543.446 208.336 532.946 176.036 506.746 172.236 L 360.646 150.936 L 295.346 18.536 C 283.646 -5.064 249.746 -5.364 237.946 18.536 Z"
			transform="matrix(1, 0, 0, 1, 0, 1.4210854715202004e-14)"
		/>
	</svg>
	{#if typeof indexStarHover !== 'undefined'}
		{#if index <= indexStarHover}
			<div class="cover" style="width: 0%"></div>
		{:else}
			<div class="cover" style="width: 100%"></div>
		{/if}
	{:else if percent}
		<div class="cover" style="width: {100 - percent}%"></div>
	{/if}
</div>

<style lang="scss">
	.stars {
		position: relative;
		white-space: nowrap;
		cursor: pointer;
		svg {
			width: 24px;
		}
	}

	svg {
		fill: gold;
	}

	.cover {
		background: white;
		height: 100%;
		overflow: hidden;
		mix-blend-mode: color;
		position: absolute;
		top: 0;
		right: 0;
	}
</style>
