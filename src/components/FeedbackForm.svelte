<script>
	import { v4 as uuidv4 } from "uuid"
	import { createEventDispatcher } from "svelte"
	import RatingSelect from "./RatingSelect.svelte"
	import Card from "./Card.svelte"
	import Button from "./Button.svelte"

	const dispatch = createEventDispatcher()

	let text = ""
	let rating = 10
	let btnDisabled = true
	let min_length = 10
	let message

	// to verify that the length of the string entered is more than the min length
	const handleInput = () => {
		if (text.trim().length <= min_length) {
			message = `Text must be at least ${min_length} characters`
			btnDisabled = true
		} else {
			message = null
			btnDisabled = false
		}
	}

	// to handle change in rating from ratingselect component
	const handleSelect = (e) => {
		rating = e.detail
	}

	// to handle submit
	const handleSubmit = () => {
		// checking the length of the text again
		if (text.trim().length > min_length) {
			const newFeedback = {
				id: uuidv4(),
				text,
				rating: +rating,
				// this makes rating into a number
			}
			dispatch("feedback-append", newFeedback)
			// clear text field
			text = ""
		}
	}
</script>

<Card>
	<header>
		<h2>How would you rate your service with us?</h2>
	</header>
	<form on:submit|preventDefault={handleSubmit}>
		<RatingSelect on:rating-select={handleSelect} />
		<div class="input-group">
			<input
				type="text"
				bind:value={text}
				on:input={handleInput}
				placeholder="Tell us what you liked about us the most!"
			/>
			<!-- <button>Send</button> -->
			<Button disabled={btnDisabled} type="submit">Send</Button>
		</div>
		<!-- displaying message when the input text contains less than 10 characters -->
		{#if message}
			<div class="message">
				{message}
			</div>
		{/if}
	</form>
</Card>

<style>
	header {
		max-width: 400px;
		margin: auto;
	}

	header h2 {
		font-size: 22px;
		font-weight: 600;
		text-align: center;
	}
	.input-group {
		display: flex;
		flex-direction: row;
		border: 1px solid #ccc;
		padding: 8px 10px;
		border-radius: 8px;
		margin-top: 15px;
	}

	input {
		flex-grow: 2;
		border: none;
		font-size: 16px;
	}

	input:focus {
		outline: none;
	}

	.message {
		padding-top: 10px;
		text-align: center;
		color: rebeccapurple;
	}
</style>
