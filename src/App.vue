<template>
  <div>
    <input type="text" v-model="text" placeholder="Enter text to analyze" />
    <button @click="analyzeText">Analyze</button>
    <div v-if="sentiment">
      <p>Negative: {{ sentiment.neg }}%</p>
      <p>Neutral: {{ sentiment.neu }}%</p>
      <p>Positive: {{ sentiment.pos }}%</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      text: '',
      sentiment: null
    }
  },
  methods: {
    analyzeText() {
      axios.post('http://localhost:5000/api/analyze_text', { text: this.text })
        .then(response => {
          this.sentiment = response.data
        })
        .catch(error => {
          console.error(error)
        })
    }
  }
}
</script>
