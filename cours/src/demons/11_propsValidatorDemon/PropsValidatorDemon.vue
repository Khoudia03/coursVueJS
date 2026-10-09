<script setup>
import Article from './Article.vue';

// import ProductCard from './ProductCard.vue'

const products = [
  { id: 1, name: 'Stylo', price: 500 },
  { id: 2, name: 'Cahier', price: 1500 },
  { id: 3, name: 'Classeur', price: 3500 },
]
</script>

<template>
  <section>
    <h2>15 - Props & Validators</h2>
    <p>Le parent envoie un objet <code>product</code> au composant enfant.</p>

    <div class="grid">
     <Article v-for="p in products" :key="p.id" :product="p" :quantite="p.id*p.price"></Article>
    </div>
  </section>
</template>

<style scoped>

.grid { display: grid; gap: 12px; grid-template-columns: repeat(3, minmax(0, 1fr)); margin-top: 12px; }
@media (max-width: 900px) { .grid { grid-template-columns: 1fr; } }

</style>