<script setup>
import { reactive } from 'vue'

const client = reactive({
  fullName: '',
  phone: '',
})

function submit() {
  alert(`Client : ${client.fullName} (${client.phone})`)
}
</script>

<template>
  <section class="card">
    <h2>14 - Forms & v-model</h2>

    <form @submit.prevent="submit" class="form">
      <input v-model="client.fullName" placeholder="Nom complet" />
      <input v-model="client.phone" placeholder="Téléphone" />
      <button>Valider</button>
    </form>

    <pre>{{ client }}</pre>
  </section>
</template>

<style scoped>
.card { padding:16px; border:1px solid #eee; border-radius:12px; }
.form { display:flex; gap:10px; flex-wrap:wrap; }
input { padding:8px; border:1px solid #ddd; border-radius:8px; }
button { padding:8px 12px; }
</style>