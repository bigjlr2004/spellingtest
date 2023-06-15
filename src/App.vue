<script setup>
import data from './data'
import { computed, ref } from 'vue'
import SpeechUtterance from './components/SpeechUtterance.vue'
import SpellingScore from './components/SpellingScore.vue'

const questions = ref([...data])
const activeIndex = ref(0)
const userInput = ref('')

const handleSubmit = () => {
  const activeQuestion = questions.value[activeIndex.value]
  activeQuestion.userInput = userInput.value
  activeIndex.value++
  userInput.value = ''
}

const testFinished = computed(() => {
  return activeIndex.value >= questions.value.length
})
</script>

<template>
  <div>Spelling Test</div>
  <div v-if="!testFinished">
    <p>Word {{ activeIndex + 1 }} of {{ questions.length }}</p>
    <SpeechUtterance :word="questions[activeIndex].word" />
    <div>
      <form @submit.prevent="handleSubmit">
        <input spellcheck="false" v-model="userInput" type="text" />
        <button type="submit" class="button is-link is-info">Submit Guess</button>
      </form>
    </div>
  </div>
  <div v-else>
    <SpellingScore v-if="testFinished" :questions="questions" />
  </div>
</template>

<style scoped></style>
