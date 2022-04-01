<script>
	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte'
	import FeedbackForm from './components/FeedbackForm.svelte'
	let feedback = [
		{
			id:1,
			rating:4,
			text: 'Ang Lorem Ipsum ay ginagamit na modelo ng industriya ng pagpriprint at pagtytypeset. Ang Lorem Ipsum ang naging regular na modelo simula pa noong 1500s, noong may isang di kilalang manlilimbag and kumuha ng galley ng type at ginulo ang pagkaka-ayos nito upang makagawa ng libro ng mga type specimen.'
		},
		{
			id:2,
			rating:6,
			text: 'Nalagpasan nito hindi lang limang siglo, kundi nalagpasan din nito ang paglaganap ng electronic typesetting at nanatiling parehas.'
		},
		{
			id:3,
			rating:8,
			text: 'Sumikat ito noong 1960s kasabay ng pag labas ng Letraset sheets na mayroong mga talata ng Lorem Ipsum, at kamakailan lang sa mga desktop publishing software tulad ng Aldus Pagemaker ginamit ang mga bersyon ng Lorem Ipsum.'
		},
	]
	$: count = feedback.length
	$: average = feedback.reduce((a, {rating}) => a + rating,0) / count
	const deleteFeedback = (e) =>{
		const itemId = e.detail
		feedback = feedback.filter(item => item.id != itemId)
	}

	const handleNewFeedback = (e) =>{
		const newFeedback = e.detail
		feedback = [newFeedback, ...feedback]
	}
</script>

<main class="container">

	<FeedbackForm on:new-rating={handleNewFeedback}/>
	<FeedbackStats {count} {average} />
	<FeedbackList {feedback} on:delete-feedback={deleteFeedback}/>

</main>