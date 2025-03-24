<script>
	let {
		color = 'currentColor',
		size = 28,
		strokeWidth = 2,
		isHovered = false,
		classes = ''
	} = $props();

</script>

<div class={classes} aria-label="chevron-down" role="img">
	<svg
		xmlns="http://www.w3.org/2000/svg"
		width={size}
		height={size}
		viewBox="0 0 24 24"
		fill="none"
		stroke={color}
		stroke-width={strokeWidth}
		stroke-linecap="round"
		stroke-linejoin="round"
	>
		<path d="m6 9 6 6 6-6" class:chevron={isHovered} />
	</svg>
</div>

<style>
	path {
		transition: all 0.2s ease-in;
	}

	.chevron {
		transform: translateY(3px);
	}
</style>
