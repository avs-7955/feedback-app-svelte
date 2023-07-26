<script>
	export let count
	export let average
</script>

<div class="feedback-stats">
	<h4>{count} Reviews</h4>
	{#if average > 0}
		<h4>{average} average</h4>
	{:else}
		<h4>0 average</h4>
	{/if}
</div>

<style>
	.feedback-stats {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
</style>
