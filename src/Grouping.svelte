<script>
    export let caption;
    export let rowspan = false;
</script>

<div class="component" class:rowspan>
    <span class="shadowtext robofont mine" style="font-size: 18px; position: absolute; top: -13px; left: 10px;">{caption}</span>
    <div style="position: absolute; top: -21px; right: 12px"><slot name="header"/></div>
    <slot/>
</div>

<style>
    .component {
        border: 10px solid black;
        border-radius: 12px;
        background-color: #49244b;

        margin: 5px;
        margin-top: 16px;
        padding-bottom: 5px;
        padding-top: 15px;
        position: relative;

        width: 368px;
        
        display: flex;
        flex-direction: column;
        align-items: stretch;
    }
</style>