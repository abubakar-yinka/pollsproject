<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import CreatePollForm from './components/CreatePollForm.svelte';
	import PollList from './components/PollList.svelte';
	import Tabs from './shared/Tabs.svelte';

	//Tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = 'Current Polls'

	const tabChanger = (e) => {
		activeItem = e.detail
	}

	// //Polls
	// let polls = [
	// 	{
	// 		id: 1,
	// 		question: 'Python or JavaScript?',
	// 		answerA: 'Python',
	// 		answerB: 'JavaScript',
	// 		votesA: 9,
	// 		votesB: 15
	// 	},
	// ];

	const handleAdd = (e) => {
		// const poll = e.detail;
		// polls = [poll, ...polls];
		// console.log(polls);
		activeItem = 'Current Polls'
	}



	// const handleVote = (e) => {
	// 	// const {id, option} = e.detail;

	// 	// let copiedPolls = [...polls];
	// 	// let upvotedPoll = copiedPolls.find((poll) => poll.id === id);
	// 	// if (option === 'a') {
	// 	// 	upvotedPoll.votesA++;
	// 	// }
	// 	// if (option === 'b') {
	// 	// 	upvotedPoll.votesB++;
	// 	// }

	// 	// polls = copiedPolls;
	// }

</script>


<Header />
<main>
	<h1>Hello Yinka!</h1>
	<Tabs {activeItem} {items} on:tabChange={tabChanger}/>
	{#if activeItem === 'Current Polls'}
		<PollList />
	{:else if activeItem === 'Add New Poll'}
		<CreatePollForm on:add={handleAdd}/>
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
	
</style>