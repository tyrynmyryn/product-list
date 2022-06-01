<script>
import notFound from '@/assets/img/not-found.png';
export default {
  data() {
    return {
      notFoundImage: notFound,
    };
  },
  props: ['products'],
};
</script>
<template>
  <ul :class="$style.list">
    <li v-for="(product, index) in products" :key="index" :class="$style.item">
      <div :class="$style.wrapper">
        <img
          :src="product.image"
          alt="Изображение товара"
          :class="$style.img"
          @error="(e) => (e.currentTarget.src = notFoundImage)"
        />
        <div :class="$style.container">
          <p :class="$style.name">{{ product.name }}</p>
          <p :class="$style.description">{{ product.description }}</p>
          <p :class="$style.price">{{ product.price }} руб.</p>
        </div>
      </div>
    </li>
  </ul>
</template>

<style module lang="scss">
@import '@/styles/vars.scss';
.list {
  grid-column: 5 / -1;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: $grid-big-gap;
  row-gap: $grid-big-gap;
  list-style-type: none;
  @media (max-width: $container-medium-size) {
    grid-column: 7 / -1;
    grid-template-columns: repeat(2, 1fr);
  }
  @media (max-width: $container-small-size) {
    grid-column: 1 / -1;
    grid-template-columns: repeat(2, 1fr);
  }
}

.container {
  padding: 16px 16px calc(24px + 30px + 32px) 16px;
}

.item {
  overflow: hidden;
  width: 100%;
  border-radius: 4px;
  background-color: $white;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  transition: $transition box-shadow;
  cursor: pointer;
  &:hover {
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.16);
  }
}

.wrapper {
  position: relative;
  animation: show 0.5s;
}

@keyframes show {
  0% {
    opacity: 0;
    transform: scale(0);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

.img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  color: blue;
  font-size: 16px;
  text-align: center;
}

.name {
  font-size: 20px;
  font-weight: 600;
  line-height: 25px;
  color: $black;
  @media (max-width: $container-small-size) {
    font-size: 16px;
    line-height: 25px;
  }
}

.description {
  margin-top: 16px;
  font-size: 16px;
  line-height: 20px;
  color: $black;
  @media (max-width: $container-small-size) {
    font-size: 12px;
    line-height: 16px;
  }
}

.price {
  position: absolute;
  bottom: 24px;
  margin-top: 32px;
  font-size: 24px;
  font-weight: 600;
  line-height: 30px;
  color: $black;
  @media (max-width: $container-small-size) {
    font-size: 20px;
    line-height: 25px;
  }
}
</style>
