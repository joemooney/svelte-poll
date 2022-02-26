<script>
	import Header from './components/Header.svelte'
	import Footer from './components/Footer.svelte'
	import CreatePollForm from './components/CreatePollForm.svelte'
	import PollList from './components/PollList.svelte'
	import Tabs from './shared/Tabs.svelte'

	export let name='no name'

	let polls = [
		{
			id: 1,
			question: 'foo',
			answerA: 'x',
			answerB: 'y',
			votesA: 2,
			votesB: 3,
		}
	];

	// tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = 'Current Polls';

	// triggered on custom event
	const tabChange = (e) => {
		activeItem = e.detail;
	}

	// triggered on custom event
	const handleAdd = (e) => {
		const poll = e.detail;
		// you cannot push, you must assign for svelte reactivity
		// polls.push(poll)
		polls = [poll, ...polls]
		console.log(polls)
		activeItem = 'Current Polls'
	}

	// triggered on custom event
	const handleVote = (e) => {
		// destructure
		const {id, option} = e.detail;
		console.log('id:', id, ' option:', option);
		// work on a copy
		let copiedPolls = [...polls];
		// get a reference

		//let poll = copiedPolls.find((p) => p.id == id )

		// Note this will not work with braces without a return
		let poll = copiedPolls.find((p) => {return p.id == id} )

		console.log('found:', poll);
		if (option == 'a') {
			poll.votesA++;
		} else {
			poll.votesB++;
		}
		// trhis reassignment will cause svelte to refresh
		polls = copiedPolls;
	}

</script>

<Header/>

<main>
	<!-- receiving custom event -->
	<Tabs {activeItem} {items} on:tabChange={tabChange}/>
	<!-- switch content based on selected tab -->
	{#if activeItem === 'Current Polls'}
		<PollList {polls} on:vote={handleVote}></PollList>
	{:else}
		<CreatePollForm on:add={handleAdd}/>	
	{/if}
</main>
<Footer/>

<style>
	main {
		max-width: 660px;
		margin: 40px auto;
	}
</style>