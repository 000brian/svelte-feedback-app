<script>
	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte';
	import FeedbackForm from './components/FeedbackForm.svelte';
	let feedback = [
		{
			id: 1,
			rating: 10,
			text: 'placeholder text',
		},
		{
			id: 2,
			rating: 1,
			text: 'placeholder text',
		},
		{
			id: 3,
			rating: 7,
			text: 'placeholder text',
		},
	];
	const deleteFeedback = (e) =>
	{
		const itemId = e.detail;
		feedback = feedback.filter((item) => item.id != itemId)
	}
	const addFeedback = (e) =>
	{
		const newFeedback = e.detail
		feedback = [newFeedback, ...feedback]
	}
	$: count = feedback.length;
	$: average = feedback.reduce((a, item) => a + item.rating, 0) / feedback.length;

</script>

<main class="container">
	<FeedbackForm on:feedback-submit={addFeedback}/>
	<FeedbackStats {count} {average} />
	<FeedbackList feedback={feedback} on:delete-feedback={deleteFeedback}/>

	
</main>

<style>

</style>