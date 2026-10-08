<script setup>
import { ref } from 'vue';


    const nomComplet = ref("");
    const tel = ref("");
    let tab = ref([]);

    function ajouter()
    {
        if(!nomComplet.value.trim() || !tel.value.trim())
        {
            alert("Veuillez remplir les champs");
            return;
        }
        
        tab.value.unshift
        ({
            id: Math.random(),
            nomComplet: nomComplet.value,
            tel: tel.value
        });
        nomComplet.value = "";
        tel.value = "";
    }
</script>


<template>
  <div>
        <form action="" @submit.prevent="ajouter">
            <input type="text" v-model="nomComplet">
            <input type="text" v-model="tel">
            <button type="submit">Ajouter</button>
        </form>
        {{ tab }}

        <p class="note">Démo :  <code>v-model</code>, <code>@submit</code></p>
  </div>
</template>



<style>

</style>