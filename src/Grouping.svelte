<script>
    export let caption;
    export let vertical = false;
</script>

<div class="component" class:vertical>
    <span class="shadowtext robofont mine" style="font-size: 18px; position: absolute; top: -13px; left: 10px;">{caption}</span>
    <div style="position: absolute; top: -21px; right: 12px"><slot name="header"/></div>
    <slot/>
</div>

<style>
    .component {
        border: 10px solid black;
        border-radius: 12px;
        background-color: #49244b;

        margin-left: 5px;
        margin-right: 5px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 5px;
        padding-top: 15px;
        position: relative;

        display: flex;
        align-items: stretch;
        flex-wrap: wrap;
    }

    .vertical {
        flex-direction: column;
    }
</style>