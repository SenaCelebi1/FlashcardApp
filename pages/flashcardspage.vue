<template>
  <main id="cardapp">
        <h1>Flashcards App</h1>
        <div class="items" v-if="items.length">
            <ul>
               <li v-for="(item, index) in items" :key="index" :class="{'done' : item.done}">                   
                   <flashcard-info :question="item.question" />
                   <flashcard-info :itemTitle="item.itemTitle" />           
                    <p></p>
                </li>
            </ul>
        </div>       
        <p class="emptylist" v-else>You do not have cards. Create one!</p>   
            <Form @submit.prevent="addItem"/>       
    </main>      
</template>


<script>
import Flashcard from '../components/Flashcard.vue';
const localKey = 'cards';
    export default {
  components: { Flashcard },
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
    
    </style>