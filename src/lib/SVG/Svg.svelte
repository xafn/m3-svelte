<script lang="ts">
	export let viewBoxHeight: number;
	export let viewBoxWidth = viewBoxHeight;
	export let svgHeight: number;
	export let svgWidth = svgHeight;
</script>

<svg
	xmlns="http://www.w3.org/2000/svg"
	preserveAspectRatio="none"
	viewBox="0 0 {viewBoxHeight} {viewBoxWidth}"
	style:height={svgHeight+'px'}
	style:width={svgWidth+'px'}
>
	<slot />
</svg>

<style lang="scss">
    svg {
        margin: 0;
        padding: 0;
    }
</style>