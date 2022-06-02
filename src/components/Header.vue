<script>
import Sort from '@/components/Sort.vue';
export default {
  props: ['sort', 'sortValues'],
  components: {
    Sort,
  },
};
</script>
<template>
  <header :class="$style.header">
    <h1 :class="$style.title">Добавление товара</h1>
    <Sort @sort="sort" :sortValues="sortValues" />
  </header>
</template>

<style module lang="scss">
@import '@/styles/vars.scss';
.header {
  display: flex;
  justify-content: space-between;
  align-self: center;
  grid-column: 1 / -1;
  margin-bottom: 16px;
  @media (max-width: $container-small-size) {
    flex-direction: column;
  }
}

.title {
  font-size: 28px;
  line-height: 35px;
  color: $black;
  @media (max-width: $container-small-size) {
    font-size: 20px;
    line-height: 25px;
  }
}
</style>
