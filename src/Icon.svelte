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
    export let onoff = false;
    export let boolean = false;
    export let caption = "";
    export let smalltext = false;
    export let smallertext = false;
    export let adnotation = "";
</script>

<div class={(!count && onoff && !boolean) ? 'greyedout' : ''} style="border: 1px solid black; position: relative; width: {size}px; height: {size}px;" on:click|preventDefault={() => count ? ++value : onoff ? boolean = !boolean : 0} on:contextmenu|preventDefault={() => (value > 0) ? --value : 0}>
    {#if tier !== 'none'}
        <img style="position: absolute; z-index: 1; width: {size}px; height: {size}px;" alt={tier} src={bg_by_tier(tier)}>
    {/if}
    <img style="position: absolute; z-index: 1000; top: 1px; left: 1px; width: {size - 2}px; height: {size - 2}px;" alt={src} {src}>
    <div style="position: absolute; z-index: 1001; display: flex; justify-content: center; width: {size}px; height: {size}px;">
        <span class="shadowtext" style="color: yellow; font-size: {Math.round(size * (smallertext ? 0.3 : smalltext ? 0.4 : 0.6))}px; margin: auto; font-variant-numeric: tabular-nums;">
            {#if count}
                {value}
            {:else}
                <div style="display: flex; flex-direction: column; justify-content: center;">
                {#if caption}
                    <span style="margin: auto;">{caption}</span>
                {/if}
                {#if adnotation}
                    <span style="margin: auto;" class="adnotation">{adnotation}</span>
                {/if}
                </div>
            {/if}
        </span>
    </div>
</div>

<style>
    .adnotation {
        font-size: 10px;
    }

    .greyedout {
        opacity: 0.3;
    }
</style>