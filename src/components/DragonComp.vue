<!-- 3. Lav nu en childcomponent: DragonComp.vue inde i "components"-mappen --> 
<!-- 7. I DragonComp skal I nu modtage props fra App.vue. Herefter skal I anvende dette og bygge en simpel template til dragerne, de skal som minimum indeholde id, name, Skills og vise billedet af dragen. OBS: for at "hive" data ud af props kan I:
   - Gøre på den mest kedelige og usexede måde: 
      <p>Den her drage hedder {{ props.dragonProps.name }} og er {{ props.dragonPoops.age }}</p>

   - Gøre det med destructuring: 
      const {name, age} = props.dragonProps
      <p>Den her drage hedder {{ name }} og er {{ age }}</p>

   - Gøre det på den FEDE måde hvor vi hiver reactive props ud (selvom vi ikke skal bruge det til noget her...):
      import {toRefs} from "vue"; //https://vuejs.org/api/reactivity-utilities.html#torefs
      const {name, age} = toRefs(props.dragonProps)
      <p>Den her drage hedder {{ name }} og er {{ age }}</p>
  -->
    <!-- 8. I skal nu gøre klar til noget vi skal bruge senere. Indsæt følgende nederst i DragonComp:  
  <form>
    <label for="betterName">Rename to:</label>
    <input type="text" placeholder="Better name..." id="betterName" required>
    <input type="submit" value="Update name" />
  </form> -->


<script setup>
import {ref} from "vue";

// state
// <!-- 10. Anvend til sidst v-model til at binde text-input feltet til en reaktiv variabel (state) som du skal lave, kald den f.eks. newName -->
const newName = ref("");

// props
const props = defineProps({
 dragonData: Object,
})

// <!-- 12. Lav handleSumbit og sørg for at den emitter en custom-event der hedder f.eks. "updateName" - sørg for at DragonComp "ved" at I vil emitte...hvordan fortæller man den det? Selve funktionen behøver i FØRSTE omgang ikke gøre andet end at emitte -->
// emit
const emit = defineEmits(["updateName"]);

// functions
function handleSubmit(){
 // <!-- 14. Udbyg nu DragonComp til at sende det nye navn (newName ref'en vi lavede i step 10) SAMT dragens id i payload i handleSubmit -->
 emit("updateName", newName.value, props.dragonData.id)
}



</script>

<template>
 <article>
<h3>{{ dragonData.name }}</h3>
<p class="skills">{{dragonData.Skills}}</p>
<img :src="dragonData.img_url">

<hr>
<!-- 11. Opsæt nu en eventlistener på formularen i DragonComp der lytter efter submit som kører en funktion "handleSubmit" -->
<form @submit.prevent="handleSubmit">
    <label for="betterName">Rename to:</label>
    <input type="text" placeholder="Better name..." id="betterName" v-model="newName" required>
    <input type="submit" value="Update name" />
</form>
<!-- New name her: {{ newName }} -->


 </article>
</template>

<style scoped>
  /* <!-- 9. Style det grundlæggende, men brug IKKE for lang tid på styling, det KUNNE se sådan her ud: https://prnt.sc/spZH-GvZ4r5E --> */

article{
 border: 2px solid red;
 border-radius: 6px;
 padding: 1rem;
 display: flex;
 flex-direction: column;
 justify-content: space-between;
 align-items: center;
}

img{
 width: 90%;
 margin: 5%;
}

</style>