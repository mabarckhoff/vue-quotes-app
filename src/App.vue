<template>
   <div id="app" class="container">
    <h1>Random Quote Generator</h1>

    <p v-if="loading">Loading...</p>
    <div v-else>
      <p>"{{ quote }}"</p>
      <p class="author">— {{ author }}</p>
    </div>

    <button @click="getQuote">Get New Quote</button>
  </div>

</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      quote: '',
      author: '',
      loading: false
    }
  },
  methods: {
    async getQuote() {
      this.loading = true
      try {
        const response = await axios.get('https://quotes15.p.rapidapi.com/quotes/random/?language_code=en', {
            headers: {
              'x-rapidapi-host': 'quotes15.p.rapidapi.com',
              'x-rapidapi-key': '52fa09b461mshdbcb0513dbbe72ep10c9ddjsnab495abd3774'
      
      },  
    });
        console.log(response)
        this.quote = response.data.content
        this.author = response.data.originator.name
      } catch (error) {
        console.error('Error fetching quote:', error)
        this.quote = 'Oops! Something went wrong.'
        this.author = ''
      } finally {
        this.loading = false
      }
    }
  },
  mounted() {
    this.getQuote()
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
container {
  text-align: center;
  font-family: Arial, sans-serif;
  margin-top: 50px;
}
button {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 16px;
}
.author {
  font-style: italic;
  font-weight: bold;
  color: #555;
  margin-top: 5px;
}

</style>
