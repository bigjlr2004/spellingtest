<script setup>
const props = defineProps(['word'])

const sayWord = () => {
  const utterance = new SpeechSynthesisUtterance(props.word)
  console.log(props.word)
  speechSynthesis.speak(utterance)
}
</script>

<template>
  <button @click="sayWord" class="clickable">Say Word</button>
</template>

<style></style>
