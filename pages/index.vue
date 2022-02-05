<template>
<div> 
  <!-- trying to think of what kind of graphic can go here, I would have to design some sort of logo or somethign which I would do later I think -->
  <Header :show="false" :function="getData" :query="query"/>
  <div v-if="resultsLength" class="container">
    <b-form-checkbox v-model="manga" name="check-button" switch>
      <!-- I was gonna have the name of the label changed to symbolize what type of search is being done,
      I figure it's better if I just define what the button does. -->
     Manga search
    </b-form-checkbox>
    <b-input-group size="lg" class="mt-3">
      <input v-on:keydown.enter="submit" v-model="query" class="searchbar" :placeholder="manga ? 'Search Manga title' : 'Search Anime title'">
      <!-- Note: When I wanted this button to be disabled, it would work fine, EXCEPT for the area where the ICON was, could not find any info about this and so I figure I had to take matters into my own hand, and just make a NEW button element that did NOT have a link...-->
      <b-button v-on:click="getData" v-if="!disableButton" class="search-button" variant="info"><b-icon icon="search"></b-icon></b-button>

      <b-button 
      v-else 
      disabled 
      class="search-button" 
      variant="info" 
      title="Your search query must have at least three (3) characters">
        <b-icon icon="search"></b-icon>
      </b-button>

    </b-input-group>
    <div class="mt-3">
      <!-- <b-button class="mb-3" variant="info">Feeling lucky?</b-button> -->
      <!-- considered doing a random button, but a lot of the id values of the different titles are not accumulative ( id number 1 will exist but not 2, 3, or 4, among others) -->
      <h5 v-if="loading"><b-spinner label="spinning" variant="info"></b-spinner> Fetching Data...</h5>
      <h5 v-else-if="errored">An error occured :(</h5>
      <p v-else>Type in the search bar the title you wish to look up! Change to a Manga search with the switch above! </p>

    </div>
  </div>

  <Results 
  v-else
  :titles="results"
  :query="query"
  :manga="manga"
  />

</div>
</template>

<script>
import axios from 'axios'
export default {
  layout: 'noToolbar',
  data() {
    return {
      manga: false,
      results: [],
      errored: false,
      loading: null,
      query: '',
    }
  },
  head() {
    return {
      meta: [
        {
          hid: 'Default query and results page',
        }
       ]
    }
  },
  computed: {
    disableButton: function () {
        return (this.query.length < 3) ? true : false;
    },
    searchType: function () {
        return (this.manga) ? 'manga' : 'anime';
    },
    resultsLength: function () {
      return this.results.length === 0
    },
  },
  methods: {
    submit () {
      if (this.disableButton == false) this.getData();
    },
    getData() {
      this.loading=true;
      axios
      //currently, only 48 results will be rendered, until pagination is figured out (lots of results render less relevant ones the more there are anyhow)
      //NSFW results are automatically omitted
    .get(`https://api.jikan.moe/v4/${this.searchType}?q=${this.query}&page=1&sfw&limit=24`)
    .then(response => (this.results = response.data.results))
    .catch(error => { 
      console.log(error)
      this.errored = true
    })
    .finally(() => this.loading = false)
    }
  }
}
</script>

<style lang="scss">

.container {
  margin: 0 auto;
  min-height: 40vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

input {
  width: 100%;
  height: 60px;
  border-radius: 10px;
  padding: 30px;

 &:focus {
   outline-width: 0;
 }
}

.search-button {  
  position: absolute;
  right: 0;
  top: 0;
  text-align: center;
  width: 90px;
  height: 64px;
  border-radius: 0 10px 10px 0;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

</style>
