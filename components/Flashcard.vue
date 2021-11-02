<template>
<main id='flashcard-info'>
    <div class="py-32 relative w-96 h-96 mx-auto mt-8 mb-8 cursor-pointer text-center font-bold tracking-light text-lg">
      <div @click="flipped = !flipped" class="card absolute text-center py-16 bg-gradient-to-br from-blue-400 via-blue-200 to-transparent overflow-hidden inset-0 rounded-lg shadow-lg" >
           {{question}}
           
         </div>
        <div v-if="flipped" class="card absolute text-center py-16 bg-gradient-to-br from-white via-green-100 bg-green-300 overflow-hidden inset-0 rounded-lg shadow-lg" @click="flipped = false">
            {{itemTitle}}                       
         </div>
   </div>
</main>
   
</template>

<script>
export default {
     
     props: ['question','itemTitle'],

        data() {
            return {
                flipped: false,                          
            }       
        }
}
</script>



