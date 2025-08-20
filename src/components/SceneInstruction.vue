<script setup>
import { onMounted, useTemplateRef } from 'vue'


const props = defineProps({
  ifButtonOnFocus: Boolean
});

defineEmits(['koniec-instrukcja', 'koniec-instrukcja-focus'])

const infoToFocuse = useTemplateRef('info-instrukcja')
onMounted(() => {
  
  //dodanie warunku propsu
  if (props.ifButtonOnFocus === true) {
    infoToFocuse.value.focus();
  }
})

const textToDisplay = "Gra składa się z dwóch poziomów – łatwego i trudnego." +
  " Rzucasz kostką i posuwasz się do przodu o tyle pól, ile oczek wyrzuciła kostka." +
  "Na początku gry otrzymujesz trzy szanse."

const textToDisplay2 = "– na polach oznaczonych znakiem zapytania czeka Cię pytanie."

const textToDisplay3 = "– na polach oznaczonych znakiem wykrzyknika  czekają Cię zasadzki." +
  "Każda błędna odpowiedź – to strata 1 szansy." +
  "Utrata wszystkich szans oznacza zakończenie gry. Dobra odpowiedź – to kolejny rzut kostką." +
  "Powodzenia!"
</script>
<template>
  <div class="tlo1" aria-label="Zasady gry">
    <div class="container">
      <div class="info-instrukcja" ref="info-instrukcja" tabindex="0">

      </div>
    </div>
      <button class="dalej my-button anim1" @click="$emit('koniec-instrukcja')" @keydown.enter="$emit('koniec-instrukcja-focus')"
    role="button">Dalej</button>
  </div>


</template>

<style scoped>
.tlo1 {
  background-image: url("../assets/Plansza_pod_instruckje_i_wybor_poziomow.png");
  background-size: 1920px 1080px;
  height: 1080px;
  width: 1920px;
  top: 0px;
  left: 0px;
  position: absolute;
}

.container{
  position: absolute;
  height: 900px;
  width: 1000px;
  background-color: white;
  top:85px;
  left:840px;
    border: 4px solid black;
  border-radius: 25px;
}

.info-instrukcja {
  height: 750px;
  width: 910px;
  top: 40px;
  left: 40px;
  position: absolute;
  border: 4px solid rgb(0, 0, 0);

}

.dalej {
    font-size: 4.3em;
    font-style: bold;
    font-weight: 700;
    font-family: "Proxima Nova", sans-serif;
    border-radius: 50px;
    width: 4em;
    height: 1.5em;
    border: 4px solid rgb(0, 0, 0);
    background-color: rgb(225, 178, 0);
    overflow: visible;
    position: absolute;
    top:940px;
    left: 1200px;
    z-index: 2;
}

.dalej:focus {
  /* border: 4px solid #08e926; */
  /* outline: thick double #08e926; */
  outline: 5px solid #e90808;
}


/* The animation code */
@keyframes example {

  from {
    opacity: 0;
  }

  to {
    opacity: 100;
  }
}

/* The element to apply the animation to */
.anim1 {
  animation-name: example;
  animation-duration: 1s;
}
</style>