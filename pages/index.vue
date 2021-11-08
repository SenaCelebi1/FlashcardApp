<template>
<div>
<input-form @sendToData="updateList($event)"/>         
<flashcard v-for="(item,index) in contentOfCards" :key="index" :item="item"/>          
    
</div>
 
</template>


<script>


import InputForm from '../components/InputForm.vue';
const localKey = 'a';

export default {

components:{
Flashcard,
InputForm
},
data(){
  return{    
    contentOfCards:[{question:'a',answer:'b',done:null},{question:'a',answer:'b',done:null}]
    
  };
  
},
methods:{
 updateList(e){

    if (!e.ques || !e.ans) {
        return; 
    }
    
  

  this.contentOfCards.push({
        question: e.ques,
        answer: e.ans,
        done: false                   
    });
    
    
 }
 
      }, 
      
      mounted() {
            const items = localStorage.getItem(localKey) || '[]';
            this.contentOfCards = JSON.parse(items);
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
