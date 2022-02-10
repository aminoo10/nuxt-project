<template>
  <article class="card">
    <div class="card__img">
      <img :src="item.images.webp.image_url" :alt="item.title">
    </div>

    <div class="card__title">
      <!-- It took me a very LONG time to understand that when you pass things through like this, it doesn't pass in the actual Boolean variable type information, it will only pass it in
      as a STRING... I had been assuming it was a boolean and wondering why it was always showing up as true, it took me a moment to realize I need to translate the string into a boolean to be able to utilize it... -->
      <nuxt-link :to="{path: '/title', query: {id: item.mal_id, manga: manga}}">
        <span>{{ item.title }}</span> 
      </nuxt-link>
    </div>
  </article>
</template>

<script>
export default {
  props: {
    item: Object,
    manga: Boolean,
  }
}
</script>

<style lang="scss" scoped>
.card {
  height: 430px;
  width: 250px;
  margin: 10px;
  border-radius: 8px;
  background: rgba(28, 162, 182, 0.192);
  overflow: hidden;
	&__img {
    height: 360px;
    width: 100%;

    img {
      height: 100%;
      width: 100%;
      object-fit: cover;
      border-radius: 0px;
    }
  }
  
  * {
    color:  rgb(16, 120, 136);
  }

	&__title {
    height: 100px;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    color:  rgb(16, 120, 136);
    font-weight: 700;

    span {
      text-overflow: ellipsis;
      overflow: hidden;
      font-size: 1rem;
    }
	}
}




</style>