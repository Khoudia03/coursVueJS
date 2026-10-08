<script setup>
import { reactive } from 'vue';


const items = reactive([]);

</script>

<template>
  <section class="card">
    <h2>12 - Conditional Rendering</h2>

    <!-- <p v-show="items.length===0">
      🛒 Panier vide
    </p> -->
    <p v-if="items.length===0">
      🛒 Panier vide
    </p>

    <ul v-else>
      <li v-for="(i, index) in items" :key="index">
        {{ i }}
      </li>
    </ul>

    <button @click="items.push('produit ' + (items.length+1))">
      Ajouter produit
    </button>
  </section>
</template>

<style scoped>
.card { padding:16px; border:1px solid #eee; border-radius:12px; }
button { margin-top:10px; padding:8px 10px; }
</style>