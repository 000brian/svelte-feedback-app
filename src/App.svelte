<script>
	import FeedbackList from './components/FeedbackList.svelte'
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
		console.table(e.detail);
		feedback = feedback.filter((item) => item.id != itemId)
	}
	$: count = feedback.length;
	$: average = feedback.reduce(() =>, 0)

</script>

<main class="container">
	<h1>{count}</h1>
	<FeedbackList feedback={feedback} on:delete-feedback={deleteFeedback}/>

	
</main>

<style>

</style>