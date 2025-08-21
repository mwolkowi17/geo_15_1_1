<script setup>
import { ref, onMounted } from 'vue'
import SceneStart from './SceneStart.vue'
import SceneLevelOneChoise from './SceneLevelOneChoise.vue'
import SceneInstruction from './SceneInstruction.vue'
import SceneMain1 from './SceneMain1.vue';

const if_plansza_poczatkowa = ref(false)
const if_instrukcja = ref(false)
const if_level_one_choise = ref(false)
const if_main1 = ref(true)


//flagi sterujące focusem w komponentach
const ifInstructionFocusOn = ref(false)
const ifLevelOneChoiseFocusOn = ref(false)
const ifMain1FocusOn = ref(false)

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

function change_level_one_choise() {
    console.log("wybrano level 1")
    // if_end_scene_level_one.value = false;
    // if_loose_after_level_one.value = false
    if_level_one_choise.value = false;
    //if_level_two_choise.value = false;
    //if_main2.value = false
    if_main1.value = true;
}

function change_level_one_choiseFocusOn() {
    ifMain1FocusOn.value = true
    setTimeout(() => {
        console.log("wybrano level 1 focus")
        // if_end_scene_level_one.value = false;
        // if_loose_after_level_one.value = false
        if_level_one_choise.value = false;
        //if_level_two_choise.value = false;
        //if_main2.value = false
        if_main1.value = true;
    }, 500)
}

function koniec_etapu1() {

    ifInFocusGlobal.value = false
    ifLevelTwoChoiseFocusOn.value = false
    ifMain1FocusOn.value = false
    if (if_main1.value) {
        if_main1.value = true;
        //if_level_two_choise.value = true;

        if_end_scene_level_one.value = true;
    } else {
        if_win.value = true;
    }
}

function koniec_etapu1_focus() {
    ifInFocusGlobal.value = true
    ifLevelTwoChoiseFocusOn.value = false
    ifMain1FocusOn.value = false
    if (if_main1.value) {
        if_main1.value = true;
        //if_level_two_choise.value = true;
         setTimeout(()=>{
      if_end_scene_level_one.value = true;
    })

    } else {
        setTimeout(()=>{
        ifWinFocusOn.value=true
        if_win.value = true;
         })
    }
}

function loose_after_level_one() {
    ifLevelOneChoiseFocusOn.value = false
    ifInFocusGlobal.value = false
    ifMain1FocusOn.value = false
    setTimeout(() => {
        if_loose_after_level_one.value = true;
    }, 500)

}

function loose_after_level_one_focus() {
    ifInFocusGlobal.value = true
    ifLevelOneChoiseFocusOn.value = false
    ifMain1FocusOn.value = false
    setTimeout(() => {
        if_loose_after_level_one.value = true;
    }, 500)

}
</script>

<template>
    <main>
        <div>
            <SceneStart v-if="if_plansza_poczatkowa" @koniec-planszy="change()" @instrukcja-focus="changeFocusOn" />
            <SceneInstruction v-if="if_instrukcja" @koniec-instrukcja="change_instrukcja()"
                @koniec-instrukcja-focus="changeInstrukcjaFocusOn" :ifButtonOnFocus="ifInstructionFocusOn" />
            <SceneLevelOneChoise v-if="if_level_one_choise" @wybor-levelu1="change_level_one_choise"
                @wybor-levelu1-focus="change_level_one_choiseFocusOn"
                :ifButtonOnFocusLevelOne="ifLevelOneChoiseFocusOn" />
            <SceneMain1 v-if="if_main1" @koniec-etap1="koniec_etapu1" @koniec-etap1-focus="koniec_etapu1_focus"
                @przegrana="loose_after_level_one" @przegrana-focus="loose_after_level_one_focus"
                :ifButtonOnFocusMain1="ifMain1FocusOn" />
        </div>
    </main>
</template>

<style scoped></style>