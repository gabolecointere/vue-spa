<template lang="html">
  <div class="">
    <button class="btn btn-primary" @click="onGetQuotes">Get quotes</button>
    <hr>
    <app-quote
                  v-for="quote in quotes"
                  :qt="quote"
                  @quoteDeleted="onQuoteDeleted($event)"></app-quote>
  </div>

</template>

<script>
import Quote from './quote.vue'
import axios from 'axios'
export default {
  data(){
    return {
      quotes: []
    }
  },
  methods: {
    onGetQuotes(){
      axios.get('http://localhost:8000/api/quotes')
      .then(
        response => {
          this.quotes = response.data.quotes
        }
      ).catch(
        error => console.log(error)
      )
    },
onQuoteDeleted(id){
  const position = this.quotes.findIndex((element) =>{
    return element.id == id
  })
  this.quotes.splice(position, 1)
}
  },
  components: {
    'app-quote': Quote
  }
}
</script>

<style lang="css">
</style>
