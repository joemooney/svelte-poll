<script>
    // for dispatching custom events
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let items;
    export let activeItem;

</script>

<div class="tabs">
    <ul>
        <!-- example of svelte each loop -->
        {#each items as item} 
        <!-- dispatch custom event, item is the data we are sending -->
        <li on:click={() => dispatch('tabChange', item)}>
            <!-- example of conditional class -->
            <div class:active={item === activeItem}> {item} </div>
        </li>
        {/each}
    </ul>
</div>


<style>
    .tabs {
        margin-bottom: 40px;
    }
    ul {
        /* auto li tags left/right */
        display: flex;
        justify-content: center;
        padding: 0;
        /* no circle icon on li */
        list-style-type: none;
    }
    li {
        margin: 0 16px;
        font-size: 18px;
        color: #555;
        /* hand */
        cursor: pointer;
    }
    .active {
        color: #d91b42;
        border-bottom: 2px solid #d91b42;
        padding-bottom: 8px;
    }

</style>