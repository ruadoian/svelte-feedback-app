<script>
   import {createEventDispatcher} from 'svelte' 
   import {v4 as uuidv4} from 'uuid'
   import Button from './Button.svelte'
    import Card from './Card.svelte'
    import RatingSelect from "./RatingSelect.svelte"

    const dispatch = createEventDispatcher()

    let text = ''
    let rating = 0
    let btnDisabled = true
    let min = 10
    let errorMsg = ''
    const handleInput = () =>{
        if(text.trim().length <= 10){
            errorMsg = `Text must be at-least ${min}`
            btnDisabled = true
        }else{
            errorMsg = null
            btnDisabled = false
        }
    }

    const handleSelect = e => rating = e.detail;

    const handleSubmit = () =>{
        if(text.trim().length > min){
            const newFeedback = {
                id: uuidv4(),
                text,
                rating: +rating
            }

            dispatch('new-rating',newFeedback)

            text = ''
        }
    }
    
</script>

<Card>
    <header><h2>How would you rate our services?</h2></header>
    <RatingSelect on:rating-selected={handleSelect}/>
    <form on:submit|preventDefault={handleSubmit}>
        <div class="input-group">
            <input type="text" on:input = {handleInput} bind:value = {text} placeholder="Tell us something that keeps you coming back">
            <Button type='submit' disabled={btnDisabled}>Send</Button>
        </div>
        {#if errorMsg}
        <div class="message">{errorMsg}</div>
        {/if}

    </form>
</Card>

<style>
    header{
        max-width: 400px;
        margin: auto;
    }
    .input-group{
        display: flex;
        flex-direction: row;
        border: 1px solid #ccc;
        padding: 8px 10px;
        border-radius: 10px;
        margin-top: 15px;
    }
    input{
        flex-grow: 2;
        border: none;
        font-size: 16px;
    }

    input:focus {
    outline: none;
  }
  .message{
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>