<script context="module">
    function bg_by_tier(tier) {
        return `Bg${tier.charAt(0).toUpperCase() + tier.slice(1)}.png`;
    }
</script>

<script>
    export let src;
    export let tier;
    export let size;
    export let count = false;
    export let value = 1;
    export let hasborder = false;
    export let caption = "";
    export let smalltext = false;
</script>

<div class:hasborder style="position: relative; width: {size}px; height: {size}px;" on:click|preventDefault={() => ++value} on:contextmenu|preventDefault={() => (value > 0) ? --value : 0}>
    {#if tier !== 'none'}
        <img style="position: absolute; z-index: 1; width: {size}px; height: {size}px;" alt={tier} src={bg_by_tier(tier)}>
    {/if}
    <img style="position: absolute; z-index: 1000; top: 1px; left: 1px; width: {size - 2}px; height: {size - 2}px;" alt={src} {src}>
    <div style="position: absolute; z-index: 1001; display: flex; justify-content: center; width: {size}px; height: {size}px;">
        <span class="shadowtext" style="color: yellow; font-size: {Math.round(size * (smalltext ? 0.3 : 0.6))}px; margin: auto; font-variant-numeric: tabular-nums;">
            {#if count}
                {value}
            {:else if caption}
                {caption}
            {/if}
        </span>
    </div>
</div>

<style>
    .hasborder {
        border: 1px solid black;
    }
</style>