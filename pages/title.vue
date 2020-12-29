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
            <div class="mb-2" v-if="manga">
              <span  v-for="author of authors" :key="author.mal_id"> {{author.name}}. </span>
            </div>
            <h5> <i>{{title.title_japanese}}</i> </h5>
            <h6> {{ title.rating }} </h6>
            <hr>
            <b-row cols="1" cols-md="2" no-gutters>
              <b-col>
                <div class="column-two__left">
                  <p v-if="manga"> Chapters<span class="value"> {{ title.chapters }} </span> </p>
                  <p v-else> Episodes<span class="value"> {{ title.episodes }} </span> </p>
                  <p v-if="manga"> Start <span class="value">{{title.published.from | substring }}</span></p> 
                  <p v-else> Start <span class="value">{{ title.aired.from | substring }}</span></p> 
                  <p> Status <span class="value">{{ title.status }}</span> </p>
                </div>
                  </b-col>
                  <b-col>
                <div class="column-two__right">
                  <p> Format <span class="value">{{ title.type }}</span> </p>
                  <p v-if="manga"> End <span class="value">{{ title.published.to | substring}}</span> </p>
                  <p v-else> End <span class="value">{{ title.aired.to | substring}}</span> </p>
                  <p> Score <span class="value"> {{ title.score }}</span></p>
                </div>
              </b-col>
              </b-row>
            <hr>
            <div class="synopsis">
              <h5>Synoposis</h5>
              <p class="mt-3"> {{title.synopsis}} </p>
            </div>
            <div class="genres mt-5">
              <p v-for="genre of this.title.genres" :key="genre.mal_id"> {{genre.name}}</p>
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
      errored: false
    }
  },
    head() {
    return {
      title: this.title.title,
      meta: [
        {
          hid: `an individual title listing of series named ${this.title.title}`,
        }
       ]
    }
  },
  mounted() {
    axios
    .get(`https://api.jikan.moe/v3/${this.searchType}/${this.$route.query.id}`)
    .then(response => (this.title = response.data))
    .catch(error => {
      console.log(error)
      this.errored = true
    })
    .finally(() => this.loading = false)
  },
  computed: {
    authors: function () {
      return this.manga ? this.title.authors : '';
    },
    searchType: function()  {
      return (this.manga) ? 'manga' : 'anime';
    },
    manga: function () {
      return (this.$route.query.manga === 'true') ? true : false;
    }
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

<style lang="scss" scoped>
$md-size: 767px;
$grid-color:  rgba(28, 162, 182, 0.192);

@mixin grid-style($order) {
  @if $order == odd {
    &:nth-child(odd) {
      background: $grid-color;
      //If I used the 'padding' property I would overwrite the one being
      //used for the '&__left, &__right' selector.
      padding-top: 1rem;
      padding-bottom: 1rem; 
    } 
  }

  @if $order == even {
    &:nth-child(even) {
      background: $grid-color;
      padding-top: 1rem;
      padding-bottom: 1rem; 
    } 
  }
}

*{
  color: rgb(16, 120, 136);
}

.container {
  margin: 3rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
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
  font-size: 15px;
  align-self: center;

  &__left {
    @media screen and (min-width: $md-size+1) {
      border-right: 1px solid rgba(28, 162, 182, 0.350);
      }
      
      p {
        @include grid-style(odd);
      }
  }

  &__right {
    p {
      @media screen and (min-width: $md-size+1) {
        @include grid-style(odd);
      }

      @media screen and (max-width: $md-size) {
        @include grid-style(even);
      }
    }
  }
  
  &__left, &__right {
    text-align: left;
    p {
      padding-left: 5px;
    }
  }

  .genres {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    
    p{
      margin: 5px 5px;
      padding: 0 5px;
      background: $grid-color;
      font-size: 14px;
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
