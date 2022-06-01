<script>
export default {};
</script>
<template>
  <div :class="$style.container">
    <slot></slot>
  </div>
</template>

<style module lang="scss">
@import '@/styles/vars.scss';

.container {
  position: relative;
  max-width: $container-big-size;
  padding: $container-big-padding;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat($grid-big-columns, 1fr);
  column-gap: $grid-big-gap;
  @media (max-width: $container-medium-size) {
    max-width: $container-medium-size;
  }
  @media (max-width: $container-small-size) {
    max-width: $container-small-size;
    padding: $container-small-padding;
  }
}
</style>
