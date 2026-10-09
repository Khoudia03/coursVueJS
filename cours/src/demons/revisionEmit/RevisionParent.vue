<script setup>
    import { reactive, ref } from 'vue'

    const plats = ref([
        {id:1,nom:"thiep",prix:6000,quantite:18},
        {id:2,nom:"soupou kandia",prix:3000,quantite:30},
        {id:3,nom:"yassa",prix:1500,quantite:15}
    ]);

    const afficherFormulaire = ref(false)
    const formPlat = reactive({
        id: 0, 
        nom: "",
        prix: 0,
        quantite: 0
    });   
    const platSelectionne = ref(null);
    const commandes = ref([]);
    const idCommandeActuel = ref(null);
    const quantiteCommandee = ref(1);


    function ajouterPlat()
    {
        if(!formPlat.nom.trim() || formPlat.quantite <= 0 || formPlat.prix <= 0)
        {
            return;
        } 
        plats.value.push({ ... formPlat, id: Math.random()}); 
        vider();      
    }

    function vider()
    {
        formPlat.nom = ""
        formPlat.prix = 0
        formPlat.quantite = 0
    }

    function details(plat) {
        if(platSelectionne.value === plat.id)
        {
            platSelectionne.value = null;
        }else
        {
            platSelectionne.value = plat.id;
        }
    }
    function commander(plat)
    {
        idCommandeActuel.value = plat.id;
    }
    function ajouterCommande()
    {
        //il permet de recuper le plat(getPlatById)
        const platActuel = plats.value.find(plat => plat.id == idCommandeActuel.value);
        
        if(quantiteCommandee.value > platActuel.quantite)
        {
            alert("Quantite indisponible");
            return;
        }
        idCommandeActuel.value = null; //on a ramené le boutton
    
        if(quantiteCommandee.value <= 0)
        {
            alert("erreur");
            return
        }
        platActuel.quantite-=quantiteCommandee.value;
        quantiteCommandee.value=0;
    }


</script>

<template>
    <div class="parent">
        <h2>Parent</h2>
        <h4>
            Liste des plats
            <button class="btn-plus" @click="afficherFormulaire = !afficherFormulaire">
                {{ afficherFormulaire ? '×' : '+' }}
            </button>
        </h4>
        
        <!-- Formulaire d'ajout -->
        <transition name="slide">
            <div v-if="afficherFormulaire" class="formulaire">
                <h3>Ajouter un plat</h3>
                <div class="champ">
                    <label>Nom du plat</label>
                    <input type="text" placeholder="Ex: mafé" v-model="formPlat.nom" />
                </div>
                <div class="ligne">
                    <div class="champ">
                        <label>Prix (FCFA)</label>
                        <input type="number" placeholder="Ex: 2000" v-model="formPlat.prix" />
                    </div>
                    <div class="champ">
                        <label>Quantité</label>
                        <input type="number" placeholder="Ex: 10" v-model="formPlat.quantite" />
                    </div>
                </div>
                <div class="form-actions">
                    <button class="btn-annuler" @click="afficherFormulaire = false">Annuler</button>
                    <button class="btn-ajouter" @click="ajouterPlat">Ajouter</button>
                </div>
            </div>
        </transition>

        <ul>
            <li v-for="p in plats" :key="p.id">
                <div class="infos">
                    <span class="nom">{{ p.nom }}</span>
                   <span class="prix">{{ p.prix }} FCFA</span>
               </div>
           
               <div class="actions">
                   <button class="btn-details" @click="details(p)">
                       {{ platSelectionne === p.id ? 'Masquer' : 'Détails' }}
                   </button>

                   <button v-if="idCommandeActuel != p.id" class="btn-commander" @click="commander(p)">
                       commander
                   </button>
                   <input v-model="quantiteCommandee" @keyup.enter="ajouterCommande" v-else type="number" placeholder="quantite">
               </div>

              <div v-if="platSelectionne === p.id" class="details-plat">
                  <h3>Détails du plat</h3>
                  <p><strong>Nom :</strong> {{ p.nom }}</p>
                  <p><strong>Prix :</strong> {{ p.prix }} FCFA</p>
                  <p><strong>Quantité disponible :</strong> {{ p.quantite }}</p>
              </div>
          </li>
        </ul>

    </div>
</template>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, sans-serif;
    background: #f5efe6;
}

.parent {
    max-width: 700px;
    margin: 40px auto;
    padding: 30px;
    background: #faf6ef;
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(78, 52, 46, 0.15);
    border: 1px solid #e0d3c0;
}

h2 {
    color: #4e342e;
    margin: 0 0 5px;
    font-size: 28px;
    letter-spacing: 1px;
}

h4 {
    color: #8d6e63;
    margin: 0 0 25px;
    font-weight: 500;
    font-size: 16px;
    text-transform: uppercase;
    letter-spacing: 2px;
    border-bottom: 2px solid #d7c4a8;
    padding-bottom: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

/* ✨ Bouton "+" */
.btn-plus {
    width: 34px;
    height: 34px;
    padding: 0;
    border: none;
    border-radius: 50%;
    background: #6d4c41;
    color: #faf6ef;
    font-size: 20px;
    font-weight: 700;
    line-height: 1;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    box-shadow: 0 3px 8px rgba(78, 52, 46, 0.25);
}

.btn-plus:hover {
    background: #4e342e;
    transform: scale(1.15) rotate(90deg);
    box-shadow: 0 5px 14px rgba(78, 52, 46, 0.4);
}

.btn-plus:active {
    transform: scale(0.95) rotate(90deg);
}

/* 📝 Formulaire */
.formulaire {
    background: linear-gradient(135deg, #fffaf3 0%, #f3e9d9 100%);
    border-radius: 12px;
    padding: 20px 22px;
    margin-bottom: 22px;
    border: 1px dashed #a1887f;
    box-shadow: 0 4px 12px rgba(78, 52, 46, 0.08);
}

.formulaire h3 {
    margin: 0 0 16px;
    color: #4e342e;
    font-size: 16px;
    font-weight: 600;
    letter-spacing: 0.5px;
}

.champ {
    display: flex;
    flex-direction: column;
    gap: 6px;
    flex: 1;
    margin-bottom: 14px;
}

.champ label {
    font-size: 12px;
    font-weight: 600;
    color: #8d6e63;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.champ input {
    padding: 10px 14px;
    border: 1px solid #d7c4a8;
    border-radius: 8px;
    background: #fffaf3;
    font-size: 14px;
    color: #4e342e;
    font-family: inherit;
    outline: none;
    transition: all 0.25s ease;
}

.champ input::placeholder {
    color: #bcaaa4;
    font-style: italic;
}

.champ input:focus {
    border-color: #6d4c41;
    background: #ffffff;
    box-shadow: 0 0 0 3px rgba(109, 76, 65, 0.15);
}

.ligne {
    display: flex;
    gap: 14px;
}

.form-actions {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
    margin-top: 6px;
}

.form-actions button {
    padding: 10px 22px;
    border: none;
    border-radius: 8px;
    font-size: 13px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
    letter-spacing: 0.5px;
}

.btn-annuler {
    background: #e0d3c0;
    color: #6d4c41;
}

.btn-annuler:hover {
    background: #d7c4a8;
    transform: scale(1.03);
}

.btn-ajouter {
    background: #6d4c41;
    color: #faf6ef;
}

.btn-ajouter:hover {
    background: #4e342e;
    transform: scale(1.03);
    box-shadow: 0 4px 12px rgba(78, 52, 46, 0.35);
}

.form-actions button:active {
    transform: scale(0.97);
}

/* 🎬 Animation */
.slide-enter-active,
.slide-leave-active {
    transition: all 0.35s ease;
    overflow: hidden;
}

.slide-enter-from,
.slide-leave-to {
    opacity: 0;
    transform: translateY(-15px);
    max-height: 0;
    padding-top: 0;
    padding-bottom: 0;
    margin-bottom: 0;
}

.slide-enter-to,
.slide-leave-from {
    opacity: 1;
    transform: translateY(0);
    max-height: 400px;
}

/* 📋 Liste */
ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: 14px;
}

li {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    padding: 16px 20px;
    background: linear-gradient(135deg, #fffaf3 0%, #f3e9d9 100%);
    border-radius: 12px;
    border-left: 5px solid #a1887f;
    transition: all 0.3s ease;
    box-shadow: 0 3px 8px rgba(78, 52, 46, 0.08);
}

li:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 18px rgba(78, 52, 46, 0.18);
    border-left-color: #6d4c41;
}

.infos {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.nom {
    font-size: 17px;
    font-weight: 600;
    color: #4e342e;
    text-transform: capitalize;
}

.prix {
    font-size: 14px;
    color: #8d6e63;
    font-weight: 500;
}

.actions {
    display: flex;
    gap: 10px;
}

.actions button {
    padding: 9px 18px;
    border: none;
    border-radius: 8px;
    font-size: 13px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
    letter-spacing: 0.5px;
}

.btn-details {
    background: #d7c4a8;
    color: #4e342e;
}

.btn-details:hover {
    background: #c4ad8a;
    transform: scale(1.05);
}

.btn-commander {
    background: #6d4c41;
    color: #faf6ef;
}

.btn-commander:hover {
    background: #4e342e;
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(78, 52, 46, 0.35);
}

.actions button:active {
    transform: scale(0.97);
}


.details-plat {
    flex-basis: 100%;
    width: 100%;
    margin-top: 15px;
    padding: 16px;
    background: #fffaf3;
    border: 1px solid #d7c4a8;
    border-radius: 10px;
    animation: apparition 0.3s ease;
}

.details-plat h3 {
    margin: 0 0 12px;
    color: #4e342e;
    font-size: 16px;
}

.details-plat p {
    margin: 8px 0;
    color: #8d6e63;
    font-size: 14px;
}

.details-plat strong {
    color: #4e342e;
}

@keyframes apparition {
    from {
        opacity: 0;
        transform: translateY(-8px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}

</style>