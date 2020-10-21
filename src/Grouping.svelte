<script>
    export let caption;
    export let wrap = false;

    $: iphonese = window.screen.width <= 240;
</script>

<div class="component" class:wrap>
    <span class="shadowtext robofont grouptitle" style="position: absolute; left: 10px;">{caption}</span>
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

        width: 248px;
        
        display: flex;
        flex-direction: column;
        align-items: stretch;
    }
    
    .grouptitle {
        font-size: 14px;
        top: -12px;
    }

    .wrap {
        flex-flow: wrap;
        padding-left: 4px;
        padding-right: -4px;
    }

@media (min-width: 320px) {
    .component {
        width: 308px;
    }

    .grouptitle {
        font-size: 18px;
        top: -14px;
    }
}
</style>