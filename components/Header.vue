<template>
    <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">AMLookup</b-navbar-brand> <!--tenative name until I come up with something cooler -->

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <!-- I found out I dont have to use nuxt-link items for this so that's pretty cool -->
        <b-nav-item
        v-for="navLink in navLinks"
        v-bind:key="navLink.id"
        :href="navLink.urlPath"
        >
        {{ navLink.name }}
        </b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav v-show="show" class="ml-auto">
        <b-nav-form>
      <!-- I couldn't get the search input in the header to tie in well with the search from here, so I'm going to omitt it until I can figure out a good way of implementing it -->
          <b-form-input v-on:keydown.enter="submit" v-model="query" size="sm" class="mr-sm-2 searchbar" placeholder="Search"></b-form-input>

            <b-button v-if="!disableButton" size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>

            <b-button v-else disabled size="sm" class="my-2 my-sm-0" type="submit" title="Your search must have at least three (3) characters">Search</b-button>


        </b-nav-form>
          <b-form-checkbox v-model="checked" name="check-button" switch class="ml-2">
            <span id="checkbox-color"> Manga search</span>
          </b-form-checkbox>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
export default {
  name: 'my-header',
  components: {
  },
  props: {
    show: Boolean,
    function: Function,
    query: String,
  },
  data() {
    return {
      query: '',
      navLinks: [
        {id: 1, urlPath: '/', name: 'Home'},
        {id: 2, urlPath: '/recommendations', name: 'Recommendations'}
      ]
    }
  },
    computed: {
    disableButton: {
      get() {
        return (this.query.length < 3) ? true : false;
      }
    }
  },
  methods: {
    submit () {
      if (this.disableButton == false )  this.function;
    }
  }

}
</script>

<style scoped lang="scss">

  #checkbox-color {
    color: white;
  }

</style>