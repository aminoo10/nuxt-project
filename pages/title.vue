<template>
  <div>
    <p v-if="loading">Fetching Data...</p>
    <p v-else-if="errored">An error occured :(</p>
      <b-container v-else>
        <b-row >
          <b-col md="6" class="column-one mb-2">
            <img :src="title.image_url" >
          </b-col>
          <b-col class="column-two">
            <h1> {{title.title}} </h1>
            <h5> <i>{{title.title_japanese}}</i> </h5>
            <h6> {{ title.rating }} </h6>
            <hr>
              <b-row cols="1" cols-md="2" no-gutters>
              <b-col>
            <div class="column-two__left">
              <p> Episodes<span class="value"> {{ title.episodes }} </span> </p>
              <p> Start <span class="value">{{ title.aired.from | substring }}</span></p> 
              <p> Status <span class="value">{{ title.status }}</span> </p>
            </div>
              </b-col>
              <b-col>
            <div class="column-two__right">
              <p> Format <span class="value">{{ title.type }}</span> </p>
              <p> End <span class="value">{{ title.aired.to | substring}}</span> </p>
              <p> Score <span class="value"> {{ title.score }}</span></p>
            </div>
              </b-col>
              </b-row>
            <hr>
            <div class="synopsis">
              <h5>Synoposis</h5>
              <p class="mt-3"> {{title.synopsis}} </p>
            </div>
          </b-col>
        </b-row>
      </b-container>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      loading: true,
      title: null,
      errored: false,
      query: 'kinnikuman'
    }
  },
  mounted() {
    axios
    .get(`https://api.jikan.moe/v3/anime/3272`)
    .then(response => (this.title = response.data))
    .catch(error => {
      console.log(error)
      this.errored = true
    })
    .finally(() => this.loading = false)
  },
  filters: {
    substring: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.substring(0, 10)
    }
  }
}
</script>

<style lang="scss">
$md-size: 767px;

.container {
  margin: 3rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title-card {
  background: rgba(28, 162, 182, 0.192);
  border-radius: 25px;
}

img {
  width: 100%;
  border-radius: 25px;

  @media screen and (max-width: $md-size) {
    width: 75%;
  }
}

.column-one {
  align-self: center;
}

.column-two {
  align-self: center;

  &__left {
    border-right: 1px solid rgba(28, 162, 182, 0.350);
  }

  &__right {
    &:nth-child(even) {
      background: rgba(28, 162, 182, 0.192);
    }
  }

  &__left, &__right {
    text-align: left;
    p {

      // @include grid-style-one;
      &:nth-child(odd) {
      background: rgba(28, 162, 182, 0.192);
      padding: 1rem 0 1rem 5px;
      }
      //Could be better way of implementing this but for now this works.
      &:nth-child(even) {
        padding-left: 5px;
      }
    } 
  }
}

.value {
  float: right;
  padding-right: 5px;
  font-weight: 600;
}

.synopsis {
  text-align: left;

  h5 {
    text-align: center;
  }
}
</style>
