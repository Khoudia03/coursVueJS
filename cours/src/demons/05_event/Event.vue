<script setup>
import { ref } from 'vue';


    const step = ref(1);
    const cpt = ref(0);

    function increment()
    {
        cpt.value+=step.value;
    }
    function reset()
    {
        cpt.value = 0;
    }
</script>


<template>
 <div>
     <div>
        <button @click="increment">Increment +</button>
        <button @click.right.prevent="reset">Reset</button>
     </div>

     <div>
        <input type="number" min="0" v-model.number="step" @keyup.enter="increment">
     </div>
     <h4>{{ cpt }}</h4>
 </div>
</template>



<style>

</style>