<script>
    import Button from "./ui/Button.svelte";
    import Card from "./ui/Card.svelte";
    import RatingSelect from "./RatingSelect.svelte";
    import { v4 as uuidv4 } from "uuid";
    import {createEventDispatcher} from 'svelte'
    let text = "";
    let btnDisabled = true;
    let min = 10;
    let rating = 10;
    const dispatch = createEventDispatcher()
    let message = null;

    const handleInput = () => {
        if (text.trim().length <= min) {
            message = `Text must be at least ${min} characters`;
            btnDisabled = true;
        } else {
            message = null;
            btnDisabled = false;
        }
    };

    const handleSelect = (e) => {
        rating = e.detail;
    };
    const handleSubmit = () => {
        if (text.trim().length > min) {
            const newFeedback = {
                text: text,
                rating: +rating, // turns rating into a number!
                id: uuidv4(),
            };
            console.log(newFeedback);
            dispatch('feedback-submit', newFeedback)
        }
    };
</script>

<Card>
    <header>
        <h2>How would you rate your service with us?</h2>
    </header>
    <RatingSelect on:rating-select={handleSelect} />
    <form on:submit|preventDefault={handleSubmit}>
        <!-- Rating Select -->
        <div class="input-group">
            <input
                type="text"
                on:input={handleInput}
                bind:value={text}
                placeholder="Tell us something that keeps you coming back"
            />
            <Button disabled={btnDisabled} type="submit">Send</Button>
        </div>
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
