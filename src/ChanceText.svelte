<script>
    export let caption;
    export let value;
    export let small = false;
</script>

<div style="margin-right: 5px; display: flex; flex-direction: column; justify-content: center; align-items: center;">
    <span class="shadowtext robofont {small ? 'smaller-text-caption' : 'text-caption'}" style="text-align: center;">{caption}</span>
    <span class="shadowtext {small ? 'smaller-text-value' : 'text-value'}" style="text-align: center;">{value}</span>
</div>

<style>
    .text-caption {
        font-size: 6px;
    }

    .text-value {
        width: 70px;
        font-size: 20px;
    }

    .smaller-text-caption {
        font-size: 5px;
    }

    .smaller-text-value {
        width: 50px;
        font-size: 14px;
    }

@media (min-width: 320px) {
    .smaller-text-caption {
        font-size: 6px;
    }

    .smaller-text-value {
        width: 70px;
        font-size: 20px;
    }
}
</style>