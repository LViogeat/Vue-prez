<script setup>
import { computed } from 'vue';
    const props = defineProps({
        isStarted: Boolean,
        count: Number,
        parentText: String
    })
    const double = computed(() =>  {
        return props.count * 2
    })
    const emit = defineEmits(['randomNumber'])
    function sendRandomNumber() {
        const randomNumber = Math.round(Math.random()*10)
        emit('randomNumber', randomNumber)
    }
</script>

<template>
    <div class="counter" style="margin-bottom: 2rem;">
      <h2 v-if="!isStarted">Pas commencé mec</h2>
      <h2 v-else>Eeet zé bartiii</h2>
        <p>Compteur doublé : {{ double }}</p>
    </div>

    <div class="textEmit">
        <p>Texte du parent : {{ parentText }}</p>
        <input type="text" :value="parentText" @input="(event)=> $emit('update:parentText', event.target.value)">
        <button @click="sendRandomNumber()">Chiffre aléatoire</button>
    </div>

</template>

<style>
    .textEmit {
        border: 1px solid green;
    }
</style>