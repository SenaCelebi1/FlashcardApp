<template>
    <main id="cardapp">
        <h1>Flashcards App</h1>
        <div class="items" v-if="items.length">
            <ul>
                <li v-for="(item, index) in items" :key="index" :class="{'done' : item.done}">
                    
                    <div  class="py-32 relative w-96 h-96 mx-auto mt-8 mb-8 cursor-pointer text-center font-bold tracking-light text-lg">
                        <div @click="item.flipped = !item.flipped" class="card absolute text-center py-16 bg-gradient-to-br from-blue-400 via-blue-200 to-transparent overflow-hidden inset-0 rounded-lg shadow-lg" >
                             <span class="label">{{item.title}}</span>
                        </div>
                        <div v-if="item.flipped" class="card absolute text-center py-16 bg-gradient-to-br from-white via-green-100 bg-green-300 overflow-hidden inset-0 rounded-lg shadow-lg" @click="item.flipped = false">
                            <span class="label">{{item.question}}</span>  
                        
                        </div>
                    </div>
                    <p></p>

        
                </li>
            </ul>
        </div>

        <p class="emptylist" v-else>You do not have cards. Create one!</p>

        <form @submit.prevent="addItem">
            <label for="newitem">Create Flashcards</label>
            <input  type="text" name="newitem" id="newitem" v-model="itemTitle" >
            <input type="text" name="newitem" id="newitem" v-model="question" >
            <button type="submit">Create Card</button>
        </form>
    </main>
</template>

<script>
    const localKey = 'cards';
    export default {
        data() {
            return {
                flipped: false,
                itemTitle: '',
                question: '',
                items: []
            }
        },
        methods: {
            addItem() {
                if (!this.itemTitle || !this.question) {
                    return;
                }
                this.items.push({
                    title: this.itemTitle,
                    question: this.question,
                    flipped: this.flipped,
                    done: false,
                });
                this.itemTitle = '';
                this.question = '';
                this.flipped = false;
            },
        
            changeItemStatus(index) {
                const item = this.items[index];
                this.items[index].done = !item.done;
            }
        },
        mounted() {
            const items = localStorage.getItem(localKey) || '[]';
            this.items = JSON.parse(items);
        },
        watch: {
            items: {
                deep: true,
                handler(items) {
                    localStorage.setItem(localKey, JSON.stringify(items))
                }
            }
        }
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    html, body {
        background: #f7f1f1;
        font-size: 1.1rem;
        font-family: 'Quicksand', sans-serif;
        height: 100%;
    }
    @keyframes strikeitem {
        to {
            width: calc(100% + 1rem);
        }
    }
    #cardapp {
        margin: 4rem auto;
        padding: 2rem 3rem 3rem;
        max-width: 500px;
        background: #afafaf;
        color: #FFF;
        box-shadow: -20px -20px 0px 0px rgba(100, 100, 100, .1);
    }
    #cardapp h1 {
        /*text-align:center;*/
        font-weight: normal;
        font-size: 2.6rem;
        letter-spacing: 0.05em;
        border-bottom: 1px solid rgba(255, 255, 255, .3);
    }
    #cardapp h1 span {
        display: block;
        font-size: 0.8rem;
        margin-bottom: 0.7rem;
        margin-left: 3px;
        margin-top: 0.2rem;
    }
    #cardapp .emptylist {
        margin-top: 2.6rem;
        text-align: center;
        letter-spacing: .05em;
        font-style: italic;
        opacity: 0.8;
    }
    #cardapp ul {
        margin-top: 2.6rem;
        list-style: none;
    }
    #cardapp .cardapp-move {
        transition: transform 1s;
    }
    #cardapp li {
        display: flex;
        margin: 0 -3rem 4px;
        padding: 1.1rem 3rem;
        justify-content: space-between;
        align-items: center;
        background: rgba(255, 255, 255, 0.1);
    }
    #cardapp .actions {
        flex-shrink: 0;
        padding-left: 0.7em;
    }
    #cardapp .label {
        position: relative;
        transition: opacity .2s linear;
    }
    #cardapp .done .label {
        opacity: .6;
    }
    #cardapp .done .label:before {
        content: '';
        position: absolute;
        top: 50%;
        left: -.5rem;
        display: block;
        width: 0%;
        height: 1px;
        background: #FFF;
        animation: strikeitem .3s ease-out 0s forwards;
    }
    #cardapp .btn-picto {
        border: none;
        background: none;
        -webkit-appearance: none;
        cursor: pointer;
        color: rgb(0, 0, 0);
    }
    
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