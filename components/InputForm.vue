<template>

<div class="w-full max-w-xs mx-auto mt-3 mb-3">
  <form @submit.prevent="sendData" class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2">
        Question
      </label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" v-model="questionValue" placeholder="Write you question!">
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2">
        Answer
      </label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" v-model="answerValue" placeholder="Write your answer!">
    </div>
     <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
        Create Card
     </button>
  </form>
</div>


</template>


<script>
var temp={ques:'', ans:''};
export default {
 

data(){
   return{
       questionValue:'',
       answerValue:''
   }
},
methods:{
    sendData(){
       
       temp.ques= this.questionValue;
       temp.ans=this.answerValue;
       
       this.$emit('sendToData', temp);

       temp.ques= '';
       temp.ans= '';
    
    }
}

 
}
</script>
