<script>
    import PollStore from "../stores/PollStore";
    import Button from "../shared/Button.svelte";
    import { createEventDispatcher } from "svelte";
    let fields = { question: '', answerA: '', answerB: '' };
    let errors = { question: '', answerA: '', answerB: '' };
    let valid = false;

    let dispatch = createEventDispatcher();

    const handleSubmit = () => {
        valid = true

        //Validate Question
        if (fields.question.trim().length < 5) {
            valid = false;
            errors.question = 'Question must be at least 5 characters long.';
        } else {
            errors.question = ''
        }

        //Validate Answer A
        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = 'Answer A cannot be empty.';
        } else {
            errors.answerA = ''
        }

        //Validate Answer B
        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = 'Answer B cannot be empty.';
        } else {
            errors.answerB = ''
        }

        //Add New Poll
        if (valid) {
            let poll = {
                ...fields,
                votesA: 0,
                votesB: 0,
                id: Math.random()
            }

            //save poll to store
            PollStore.update((currentPolls) => {
                return [poll, ...currentPolls]
            })
            dispatch('add');
        }
    }
</script>

<form on:submit|preventDefault = {handleSubmit}>
    <!-- The For attribute in the label generally is equal to the ID(To link the Label and Input) -->
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" id="question" bind:value={fields.question}>
        <div class="errors">{errors.question}</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A</label>
        <input type="text" id="answer-a" bind:value={fields.answerA}>
        <div class="errors">{errors.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B</label>
        <input type="text" id="answer-b" bind:value={fields.answerB}>
        <div class="errors">{errors.answerB}</div>
    </div>
    <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
    form {
        margin: 0 auto;
        width: 400px;
        text-align: center;
    }
    .form-field{
        margin: 18px auto;   
    }
    input {
        width: 100%;
        border-radius: 6px;
    }
    label {
        margin: 10px auto;
        text-align: left;
    }
    .errors {
        font-weight: bold;
        color: #d91b42;
        font-size: 12px;
    }
</style>