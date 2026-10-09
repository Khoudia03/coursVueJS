<script setup>
const props = defineProps({
    salle: Object
})
const emit = defineEmits(["supprimer", "ajout"]);

function supprimerSalle()
{
   emit("supprimer", props.salle.id); 
}
console.log(props.salle);


</script>


<template>
  <div>
    <li>
        {{ salle.salle }} - {{ salle.id }} - {{ salle.placeOccupee }} / {{ salle.capacite }}
    </li>
    <button @click="supprimerSalle">Delete</button>
    <button @click="emit('ajout', salle.id)" 
    :disabled="salle.capacite===salle.placeOccupee">+</button>
  </div>
</template>



<style>

</style>