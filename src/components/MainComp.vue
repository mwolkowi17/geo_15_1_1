<script setup>
import { ref, onMounted } from 'vue'
import SceneStart from './SceneStart.vue'
import SceneLevelOneChoise from './SceneLevelOneChoise.vue'
import SceneInstruction from './SceneInstruction.vue'

const if_plansza_poczatkowa = ref(true)
const if_instrukcja = ref(false)

//flagi sterujące focusem w komponentach
const ifInstructionFocusOn = ref(false)
const ifLevelOneChoiseFocusOn = ref(false)

//sterowanie widokami gry
function change() {
    if_plansza_poczatkowa.value = false;
    if_instrukcja.value = true;
}
//dodanie focusu
function changeFocusOn() {
    ifInstructionFocusOn.value = true
    setTimeout(() => {
        if_plansza_poczatkowa.value = false;
        if_instrukcja.value = true;
    }, 500)
}

function change_instrukcja() {
    if_instrukcja.value = false
    if_level_one_choise.value = true
}

function changeInstrukcjaFocusOn() {
    ifLevelOneChoiseFocusOn.value = true
    setTimeout(() => {
        if_instrukcja.value = false
        if_level_one_choise.value = true
    }, 500)
}
</script>

<template>
    <main>
        <div>
        <SceneStart v-if="if_plansza_poczatkowa" @koniec-planszy="change()" @instrukcja-focus="changeFocusOn" />
         <SceneInstruction v-if="if_instrukcja" @koniec-instrukcja="change_instrukcja()"
                @koniec-instrukcja-focus="changeInstrukcjaFocusOn" :ifButtonOnFocus="ifInstructionFocusOn" />
        </div>
    </main>
</template>

<style scoped>

</style>