<script setup>
import { ref, onMounted } from 'vue'
import SceneStart from './SceneStart.vue'

const if_plansza_poczatkowa = ref(true)

//flagi sterujące focusem w komponentach
const ifInstructionFocusOn = ref(false)

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
</script>

<template>
    <main>
        <div>
        <SceneStart v-if="if_plansza_poczatkowa" @koniec-planszy="change()" @instrukcja-focus="changeFocusOn" />
        </div>
    </main>
</template>

<style scoped>

</style>