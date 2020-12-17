<template>
  <div id="root-container">
    <h4 class="mt-3 ml-3">Search results for "{{query}}"</h4>
    <hr>

    <div class="container">
      <p v-if="loading">Fetching Data...</p>
      <p v-else-if="errored">An error occured :(</p>
      <Card 
        v-else
        v-for="title of titles"
        :key="title.mal_id"
        :item="title"
      />  
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      loading: true,
      titles: null,
      errored: false,
      query: 'kinnikuman'
    }
  },
  mounted() {
    axios
    //NSFW entries are automatically omitted 
    .get(`https://api.jikan.moe/v3/search/anime?q=${this.query}&genre_exclude=0&genre=12&limit=12`)
    .then(response => (this.titles = response.data.results))
    .catch(error => {
      console.log(error)
      this.errored = true
    })
    .finally(() => this.loading = false)
  }
}
</script>

<style>


.container {
  margin: 0 auto;
  min-height: 20vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: space-evenly;
  text-align: center;
}

.red-square {
  background-color: red;
  width: 5rem;
  height: 5rem;
  margin-left: 5px;
}

</style>
