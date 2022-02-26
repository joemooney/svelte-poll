<script>
    import { createEventDispatcher } from 'svelte';

    import Button from '../shared/Button.svelte'

    let dispatch = createEventDispatcher();

    let fields = {
        question: "",
        answerA: "",
        answerB: "",
    };
    let errors = {
        question: "",
        answerA: "",
        answerB: "",
    };
    let valid = false;

    const submitHandler = () => {
        valid = true;
        console.log(fields);
        if ( fields.question.trim().length < 1) {
            valid = false;
            errors.question = 'question must be at least 5 characters long';
        }
        if ( fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = 'answer A is empty';
        }
        if ( fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = 'answer B is empty';
        }

        // add new poll
        if (valid) {
            let poll = { ...fields, votesA:0, votesB:0, id: Math.random() };
            dispatch('add', poll);

            console.log('valid', fields)
        } else {

        }
    }


</script>

<!-- we do not want to submit the form, which is the default action
     so we add |preventDefault -->
<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question:</label>
        <!-- id links the label with the for -->
        <input type="text" id="question" bind:value={fields.question}>
        <div class="error">{errors.question}</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A</label>
        <input type="text" id="answer-a" bind:value={fields.answerA}>
        <div class="error">{errors.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B</label>
        <input type="text" id="answer-b" bind:value={fields.answerB}>
        <div class="error">{errors.answerB}</div>
    </div>
    <Button type='secondary'>Add Poll</Button>

</form>
<style>
    form {
        width: 400px;
        margin: 0 auto; /* auto => apply left and right */
        text-align: center;
    }
    .form-field {
        margin: 18px auto;
    }
    input {
        width: 100%;
        border-radius:  6px;
    }
    label {
        margin: 10px auto;
        text-align: left;
    }
    .error {
        font-weight: bold;
        font-style: italic;
        font-size: 12px;
        color: #d91b42;
    }

</style>