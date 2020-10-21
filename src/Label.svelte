<script>
    export let caption;
    export let value;
</script>

<div class="component">
    <div style="display: flex; justify-content: flex-start;">
        <slot/>
    </div>
    <div style="margin-top: 6px; display: flex; flex-direction: column; align-items: center; justify-content: center;">
        <span class="shadowtext robofont" style="font-size: 6px;">{caption.toUpperCase()}</span>
        <span class="shadowtext" style="font-size: 24px; width: 100px; text-align: center;">{value}</span>
    </div>
</div>

<style>
    .component {
        background-color: #4F4846;

        padding: 3px;
        margin-top: 8px;

        display: flex;
    }
</style>