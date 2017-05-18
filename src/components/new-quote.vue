<template lang="html">
  <form @submit.prevent="onSubmitted">
    <div class="form-group">
      <label for="content">Content</label>
<input type="text" class="form-control" id="content" v-model="quoteContent">
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      quoteContent: ''
    }
  },
  methods: {
    onSubmitted() {
      const token = localStorage.getItem('token')
      axios.post('http://localhost:8000/api/quote?token=' + token, {
        content: this.quoteContent
      }).then(
        (response) => console.log(response)
      ).catch(
        (error) => console.log(error)
      )
    }
  }
}
</script>

<style lang="css">
</style>
