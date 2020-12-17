<template>
  <article class="card">
    <div class="card__img">
      <img :src="item.image_url" :alt="item.title">
    </div>

    <div class="card__title">
      <span>{{ item.title }}</span>
    </div>
  </article>
</template>

<script>
export default {
  props: {
    item: Object
  }
}
</script>

<style lang="scss">
.card {
  height: 430px;
  width: 250px;
  margin: 10px;
  border-radius: 8px;
  background: #fff;
  overflow: hidden;
	&__img {
    height: 360px;
    width: 100%;

    img {
      height: 100%;
      width: 100%;
      object-fit: cover;
    }
	}

	&__title {
    height: 70px;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 14px;
    color: #343434;
    font-weight: 700;

    span {
      text-overflow: ellipsis;
      overflow: hidden;
    }
	}
}




</style>