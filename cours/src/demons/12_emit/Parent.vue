<script setup>
import { ref } from 'vue';
import Enfant from './Enfant.vue';

const trouve = ref("");
const salles = ref([
    {salle: "Dev", id: 1, capacite: 50, placeOccupee: 49},
    {salle: "Ref Dig", id: 2, capacite: 100, placeOccupee: 70}
]);

function deleteSalle(id)
{
    salles.value = salles.value.filter(salle => salle.id != id);
}
function ajoutParticipant(idSalle)
{
    const salleTrouve = salles.value.find(salle => salle.id === idSalle);
    salleTrouve.placeOccupee+=1;
    if(salleTrouve.capacite === salleTrouve.placeOccupee)
    {
        trouve.value = salleTrouve.salle;
        return;
    }
    
}
</script>


<template>
  <div>
    <Enfant v-for="s in salles" :key="s.id"
            :salle="s"
            @supprimer="deleteSalle"
            @ajout="ajoutParticipant">
            
    </Enfant>
    <p v-if="trouve">Cette Salle {{ trouve }} est pleine</p>
  </div>
</template>



<style>

</style>