<script setup>
import { computed, reactive } from 'vue';


    const cart = reactive([
        {
            nom: "stylo",
            prix: 200,
            stock: 23
        },
        {
            nom: "cahier",
            prix: 125,
            stock: 50
        },
        {
            nom: "gomme",
            prix: 50,
            stock: 100
        },
        {
            nom: "crayon",
            prix: 100,
            stock: 150
        }
    ])

    const total = computed(()=>{
        return cart.reduce((a,s)=>a+s.prix*s.stock, 0);
    });
</script>

<template>
  <section class="card">
    <h2>11 - computed()</h2>

    <ul>
      <li v-for="item in cart" :key="item.nom">
        {{ item.nom }}: {{item.prix}} × {{item.stock}} -> {{item.prix*item.stock}} FCFA
      </li>
    </ul>

    <h3>Total : {{total}} FCFA</h3>

    <p class="note">
      Le total se met à jour automatiquement.
    </p>
  </section>
</template>

<style scoped>
.card { padding:16px; border:1px solid #eee; border-radius:12px; }
.note { margin-top:8px; color:#555; }
</style>