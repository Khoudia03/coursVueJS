<script setup>
import { reactive } from 'vue';

const products = reactive([
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
    ]);

// const removeProduct = (product) => {
//   const index = products.findIndex((p) => p.nom === product.nom);

//   if (index !== -1) {
//     products.splice(index, 1);
//   }
// };
</script>

<template>
  <section class="card">
    <h2>13 - Lists</h2>

    <ul>
      <li v-for="(product,i) in products" :key="i">
      <!-- <li v-for="p in products" :key="p.nom"> -->
        {{ product.nom }} - {{ product.prix }} FCFA
        <button @click="products.splice(i,1)">❌</button>
        <!-- <button @click="products.value = products.value.filter((product) => product.nom !== p.nom)">❌</button> -->
      </li>
    </ul>
  </section>
</template>

<style scoped>
.card { padding:16px; border:1px solid #eee; border-radius:12px; }
li { display:flex; justify-content:space-between; width:250px; }
button { border:none; background:none; cursor:pointer; }
</style>