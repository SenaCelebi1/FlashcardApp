<template>

<div class="py-32 relative w-80 h-80 mx-auto mt-5 mb-5 cursor-pointer text-center font-bold tracking-light text-lg">
      
      <div @click="flipped = !flipped" class="card absolute text-center py-16 bg-gray-200 overflow-hidden inset-0 rounded-lg shadow-lg" >
           <h2 class="text-gray-800 text-3xl font-semibold">Your Question</h2>
           <p class="text-gray-600">{{item.question}}</p>  
         </div>
        
        <div v-if="flipped" class="card absolute text-center py-16 bg-gray-400 overflow-hidden inset-0 rounded-lg shadow-lg" @click="flipped = false">
            <h2 class="text-gray-800 text-3xl font-semibold">Your Answer</h2>
            <p class="text-gray-600">{{item.answer}}</p>                     
         </div>
  
   </div>





</template>


<script>
export default {

  props:{
    item:Object
  },
  data(){
    return{
     flipped: false
    }
  }
 
}
</script>
