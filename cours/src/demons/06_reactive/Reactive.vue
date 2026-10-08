<script setup>
import { reactive, ref } from 'vue';

    const obj = reactive({ 
        nom: "mami cisse",
        tel: "77777777",
        solde: 1000000
    });

    const autre = ref(0);
     let cpt = ref(0);
    function ajouter(montant)
    {
        if(cpt.value < 10)
        {
            obj.solde +=montant;
            cpt.value++;
        }
        autre.value=0;
        return;
       
    }

    

    
</script>

<template>
  <section class="card">
    <h2>09 - reactive()</h2>

    <div class="box">
      <p><strong>Nom :</strong> {{obj.nom}} </p>
      <p><strong>Téléphone :</strong> {{obj.tel}} </p>
      <p><strong>Solde :</strong> {{obj.solde}} FCFA</p>
    </div>

    <div class="actions">
      <button @click="ajouter(5000)">+5 000</button>
      <button @click="ajouter(10000)">+10 000</button>
      <input @keyup.enter="ajouter(autre)" type="number" v-model="autre" placeholder="ajouter un montant">
    </div>

    <p class="note">
      <code>reactive()</code> est idéal pour les objets complexes.
    </p>
  </section>
</template>

<style scoped>
.card { padding:16px; border:1px solid #eee; border-radius:12px; }
.box { padding:12px; background:#fafafa; border-radius:10px; }
.actions { display:flex; gap:10px; margin-top:10px; }
button { padding:8px 10px; border:1px solid #ddd; border-radius:8px; }
.note { margin-top:8px; color:#555; }
</style>