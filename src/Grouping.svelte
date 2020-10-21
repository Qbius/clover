<script>
    export let caption;
</script>

<div class="component">
    <span class="shadowtext robofont mine" style="font-size: 18px; position: absolute; top: -13px; left: 10px;">{caption.toUpperCase()}</span>
    <div style="position: absolute; top: -21px; right: 12px"><slot name="header"/></div>
    <slot/>
</div>

<style>
    .component {
        border: 10px solid black;
        border-radius: 12px;

        padding: 10px;
        position: relative;

        display: flex;
        flex-direction: column;
        align-items: stretch;
    }
</style>