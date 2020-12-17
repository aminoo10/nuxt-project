<template>
    <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">AMLookup</b-navbar-brand>

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
          <b-form-input v-if="checked" size="sm" class="mr-sm-2 searchbar" placeholder="Search Manga"></b-form-input>
          <b-form-input v-else size="sm" class="mr-sm-2 searchbar" placeholder="Search Anime"></b-form-input>

          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
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
    show: Boolean
  },
  data() {
    return {
      checked: false,
      navLinks: [
        {id: 1, urlPath: '/', name: 'Home'},
        {id: 2, urlPath: '/about', name: 'About'}
      ]
    }
  }
}
</script>

<style scoped lang="scss">

  #checkbox-color {
    color: white;
  }

</style>