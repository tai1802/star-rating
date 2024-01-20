<script lang="ts">
	import StarIcon from './StarIcon.svelte';

	export let ratingValue: number = 4.35;

	let indexStarHover: number | undefined;

	const onHoverStar = (event: CustomEvent) => {
		indexStarHover = Number(event.detail);
	};

	const onMouseLeave = () => (indexStarHover = undefined);

	const onClickStar = (event: CustomEvent) => {
		alert(event.detail);
	};
</script>

<div class="flex flex-row gap-2 w-fit" on:mouseleave={onMouseLeave} role="presentation">
	{#each Array(5) as _item, index}
		{#if ratingValue - index < 1}
			<StarIcon
				{index}
				{indexStarHover}
				percent={(ratingValue - index) * 100}
				on:hover={onHoverStar}
				on:click={onClickStar}
			/>
		{:else}
			<StarIcon
				{index}
				{indexStarHover}
				percent={100}
				on:hover={onHoverStar}
				on:click={onClickStar}
			/>
		{/if}
	{/each}
</div>
