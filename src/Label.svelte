<script>
    import ChanceText from './ChanceText.svelte';

    export let caption;
    export let value;
    export let extras = [];
    export let small = false;
</script>

<div class="component">
    <div style="display: flex; justify-content: flex-start;">
        <slot/>
    </div>
    <div style="flex: 1; margin-top: 6px; display: flex; justify-content: flex-end;">
        <ChanceText {caption} {value} {small}></ChanceText>
        {#each extras as extra}
            <ChanceText caption={extra[0]} value={extra[1]} {small}></ChanceText>
        {/each}
    </div>
</div>

<style>
    .component {
        background-color: #200f21;
        border: 1px solid black;

        padding: 3px;
        margin-bottom: 3px;
        margin-right: 5px;
        margin-left: 5px;

        display: flex;
    }
</style>