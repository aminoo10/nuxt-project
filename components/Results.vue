<!--Initially, this was going to be it's own page, but it seems to work much better as it's own component, so I made it as such being utilized by the index page -->
<template>
  <div id="root-container">
    <h4 class="mt-3 ml-3">Search results for "{{query}}"</h4>
    <hr>

    <div class="container">
      <Card 
        v-for="title of titles"
        :key="title.mal_id"
        :item="title"
        :manga="manga"
      />  
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  props: {
    titles: Object,
    query: String,
    manga: Boolean,
  },
  data() {
    return {
      titles: null,
    }
  },
}
</script>

<style lang="scss" scoped>

.container {
  margin: 0 auto;
  min-height: 20vh;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
  text-align: center;
}

.red-square {
  background-color: red;
  width: 5rem;
  height: 5rem;
  margin-left: 5px;
}


</style>
