<script>
import notFound from '@/assets/img/not-found.png';
import deleteIcon from '@/assets/icons/delete.svg';

export default {
  data() {
    return {
      notFoundImage: notFound,
      deleteIcon: deleteIcon,
      removedProduct: null,
    };
  },
  methods: {
    deleteProduct(product) {
      this.removedProduct = product.id;
      setTimeout(() => {
        this.$emit('deleteProduct', product);
      }, 500);
    },
    addThousandsSeparator(number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
  },
  props: ['products'],
  emits: ['deleteProduct'],
};
</script>
<template>
  <ul :class="$style.list">
    <li
      v-for="(product, index) in products"
      :key="index"
      :class="[
        $style.item,
        removedProduct === product.id ? $style.removedItem : '',
      ]"
    >
      <img
        @click="() => deleteProduct(product)"
        :src="deleteIcon"
        :class="$style.icon"
        alt="Удалить"
      />
      <img
        :src="product.image"
        alt="Изображение товара"
        :class="$style.img"
        @loadstart="(e) => (e.currentTarget.src = notFoundImage)"
        @error="(e) => (e.currentTarget.src = notFoundImage)"
      />
      <div :class="$style.container">
        <p :class="$style.name">{{ product.name }}</p>
        <p :class="$style.description">{{ product.description }}</p>
        <p :class="$style.price">
          {{ addThousandsSeparator(product.price) }} руб.
        </p>
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
  position: relative;
  width: 100%;
  border-radius: 4px;
  background-color: $white;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  transition: $transition box-shadow;
  cursor: pointer;
  animation: show 0.5s;
  &:hover {
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.16);
    .icon {
      opacity: 1;
      user-select: all;
    }
  }
}

.removedItem {
  animation: delete 0.5s;
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

.icon {
  position: absolute;
  top: -8px;
  right: -8px;
  padding: 8px;
  border-radius: 10px;
  background: #ff8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  opacity: 0;
  user-select: none;
  transition: $transition opacity;
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

@keyframes delete {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
</style>
