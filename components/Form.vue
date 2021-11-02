<template>
    <form >
            <label for="newitem">Create Flashcards</label>
            <input  type="text" name="newitem" id="newitem" v-model="itemTitle" >
            <input type="text" name="newitem" id="newitem" v-model="question" >
            <button type="submit">Create Card</button>
        </form>
</template>

<style >
/* FORM */
    form {
        margin-top: 3rem;
        display: flex;
        flex-wrap: wrap;
    }
    form label {
        min-width: 100%;
        margin-bottom: .5rem;
        font-size: 1.3rem;
        text-align: center;
        font-weight: bold;
    }
    form input {
        margin-top: 1rem;
        flex-grow: 1;
        border: none;
        background: #74737377;
        padding: 0 1.5em;
        font-size: initial;
        
    }
    form button {
        margin-top: 1rem;
        padding: 0 1.3rem;
        border: none;
        background: #5c59f7;
        color: white;
        text-transform: uppercase;
        font-weight: bold;
        cursor: pointer;
        transition: background .2s ease-out;     
      
    }
    form button:hover {
        background: #4e4bfd;
    }
    form input,
    form button {
        font-family: 'Quicksand', sans-serif;
        height: 3rem;
    }

</style>