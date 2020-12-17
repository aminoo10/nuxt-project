<template>
<div>
  <div class="container">
    <b-form-checkbox v-model="checked" name="check-button" switch>
      <!-- I was gonna have the name of the label changed to symbolize what type of search is being done,
      I figure it's better if I just define what the button does. -->
     Manga search
      <!-- <span v-else>Anime</span> -->
    </b-form-checkbox>
    <b-input-group size="lg" class="mt-3">
    <input v-model="search" v-if="checked" class="searchbar" placeholder="Search Manga title">
    <input v-model="search" v-else class="searchbar" placeholder="Search Anime title">
    <b-button class="search-button" variant="info"><b-icon icon="search"></b-icon></b-button>
    </b-input-group>
    <p class="mt-5">Type in the search bar the title you wish to look up! Change to a Manga search with the switch above! </p>
  </div>

</div>
</template>

<script>

export default {
  layout: 'NoSearchToolbar',
  data() {
    return {
      checked: false
    }
  }
}
</script>

<style lang="scss">
.container {
  margin: 0 auto;
  min-height: 100vh;
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
