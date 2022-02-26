<script>
    import PollDetails from './PollDetails.svelte'
    // passed prop will override
    export let polls = [];

</script>

<div class='poll-list'>
    <!-- need to register each poll with an is 2nd arg in as -->
    {#each polls as poll (poll.id)}
        <!-- since on:vote has no handler it is automagically forwarded -->
        <div><PollDetails {poll} on:vote></PollDetails></div>
    {/each}

</div>

<style>
    .poll-list {
        display: grid;
        /* one in each column */
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }

</style>