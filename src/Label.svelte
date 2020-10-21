<script>
    import ChanceText from './ChanceText.svelte';

    export let caption;
    export let value;
    export let extras = [];
</script>

<div class="component">
    <div style="display: flex; justify-content: flex-start;">
        <slot/>
    </div>
    <div style="flex: 1; margin-top: 6px; display: flex; justify-content: flex-end;">
        <ChanceText {caption} {value}></ChanceText>
        {#each extras as extra}
            <ChanceText caption={extra[0]} value={extra[1]}></ChanceText>
        {/each}
    </div>
</div>

<style>
    .component {
        background-color: #200f21;
        border: 1px solid black;

        min-width: 317px;
        padding: 3px;
        margin-bottom: 4px;

        display: flex;
    }
</style>