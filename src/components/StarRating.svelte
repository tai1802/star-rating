<script lang="ts">
	import StarIcon from './StarIcon.svelte';

	export let ratingValue: number = 4.8;

	let indexStarHover: number | undefined;

	const onHoverStar = (event: CustomEvent) => {
		indexStarHover = Number(event.detail);
	};

	const onMouseLeave = () => (indexStarHover = undefined);
</script>

<div class="flex flex-row gap-2 w-fit" on:mouseleave={onMouseLeave} role="presentation">
	{#each Array(5) as _item, index}
		{#if ratingValue - index < 1}
			<StarIcon
				{index}
				percent={(ratingValue - index) * 100}
				on:hover={onHoverStar}
				{indexStarHover}
			/>
		{:else}
			<StarIcon {index} percent={100} on:hover={onHoverStar} {indexStarHover} />
		{/if}
	{/each}
</div>
