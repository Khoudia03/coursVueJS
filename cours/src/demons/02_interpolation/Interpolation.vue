<script setup>
   
    const annee = new Date().getFullYear();
    const montant = 100000;
    const prime = 0.5

    const personne = {nom: "Konuamaru", role: "Ninja"}

</script>


<template>
  <div class="card">
        <ul>
            <li>Nom: {{ personne.nom.toUpperCase() }}</li>
            <li>Role: {{ personne.role }}</li>
            <li>Annee: {{ annee }}</li>
            <li>Prime: {{ prime }}</li>
            <li>Montant: {{ montant.toLocaleString() }} $</li>
            <li>Salaire Nette: {{ montant + montant*prime }} $</li>
        </ul>
  </div>
</template>



<style>

</style>