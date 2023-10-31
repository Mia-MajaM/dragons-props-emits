<script setup>
import { ref } from 'vue';
// <!-- 1. Importer dragerne og gem dem i state (reactive state...hvad skal vi huske at importere for at gøre data reactive?) - de ligger i assets/dragons.js -->
import dragonData from "./assets/js/dragons"

// <!-- 4. Importér din nye childcomponent i App.vue -->
import DragonComp from "./components/DragonComp.vue"

// state
const dragons = ref(dragonData);

// <!-- 15. Modtag nu payload(s) i App.vue og log dem -->
// functions
function handleUpdate(awesomeNewName, dragonId){

  // <!-- 16. Udbyg nu i App.vue så:
  //       - Den korrekte drage findes ud fra det id der er sendt i payload (anvend .find(): https://www.w3schools.com/jsref/jsref_find.asp)
  //       - Denne drages name skal nu opdateres med det name der er sendt i payload fra DragonComp
  // -->
  // find den rigtigdrage, der skal have ændret navn
const correctDragon = dragons.value.find(
  function(dragon){
return dragon.id == dragonId
  }
  )

  // opdater dens navn
  correctDragon.name = awesomeNewName;
}

</script>

<template>
  <!--  -->
  <!-- Del 1: props. 1 til 10 -->
  <!--  -->
  
  <!--  -->
  <!-- Del 2: emits 11 til 17-->
  <!--  -->
 
  



  <!-- 17. Ekstra/evt: lav en mulighed for at delete dragerne i DragonComp. Så de sender en anden custom event og App.vue fjerner den relevante drage fra state. Se her: https://youtu.be/uXvypD2gPjw -->

  <header>
    <h1>DnD website</h1>
  <!-- 2. I App.vue i <h2> sørg for tallen indsættes dynamisk: se eksempel her: https://prnt.sc/XTygZonF7YCX -->
    <h2>
      Your source for DnD dragons. Providing dragon information since 2021.<br />
      Find info about <span>{{dragons.length}}</span> dragons here.
    </h2>
  </header>
  <main>
    <!-- Indsæt drager her... -->
 <!-- 5. Loop igennem state med listen af drager og lav en DragonComp for hver -->
  <!-- 6. Send "dragedata" fra App.vue NED til dine childcomponents - send alt data, det vil sige send drage-objektet--> <!-- :dragonData="dragon"  -->
   <!-- 13. Lyt nu denne custom event i App.vue og kald en funktion når den indtræder, log til konsol i denne funktion --><!--@updateName="handleUpdate"  -->
  <DragonComp @updateName="handleUpdate" v-for="dragon in dragons" :key="dragon.id" :dragonData="dragon"></DragonComp>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  min-height: 60vh;
  background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.9)), url("@/assets/img/bg_dragon.jpg");
  background-size: cover;
  display: grid;
  place-content: center;
  color: white;
}

h1 {
  font-size: 4rem;
}

span {
  color: crimson;
}

main {
  max-width: 1000px;
  margin: 1rem auto;
  padding: 2rem;
  box-shadow: 0 0 3px 1px rgba(0, 0, 0, 0.3);
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  border-radius: 6px;
}

@media screen and (max-width: 1050px) {
  main {
    grid-template-columns: 1fr;
    padding: 5rem;
  }
}
</style>
