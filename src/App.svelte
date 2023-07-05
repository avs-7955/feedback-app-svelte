<script>
	import FeedbackForm from "./components/FeedbackForm.svelte"
	import FeedbackList from "./components/FeedbackList.svelte"
	import FeedbackStats from "./components/FeedbackStats.svelte"
	let feedback = [
		{
			id: 1,
			rating: 10,
			text: "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Sed illum placeat blanditiis eos, voluptate excepturi impedit facere!",
		},
		{
			id: 2,
			rating: 9,
			text: "Sed illum placeat blanditiis eos, voluptate excepturi impedit facere!",
		},
		{
			id: 3,
			rating: 8,
			text: "Lorem ipsum, dolor sit amet consectetur adipisicing elit.",
		},
	]

	// feedback stats
	$: count = feedback.length
	$: average =
		feedback.reduce((a, { rating }) => a + rating, 0) / feedback.length

	// deleting the feedback
	const deleteFeedback = (e) => {
		const itemId = e.detail
		feedback = feedback.filter((item) => item.id != itemId)
	}

	const addFeedback = (e) => {
		const newFeed = e.detail
		feedback = [newFeed, ...feedback]
	}
</script>

<main class="container">
	<FeedbackForm on:feedback-append={addFeedback} />
	<FeedbackStats {count} {average} />
	<FeedbackList {feedback} on:delete-feedback={deleteFeedback} />
</main>
