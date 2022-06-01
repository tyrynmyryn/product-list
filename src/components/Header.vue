<script>
export default {};
</script>
<template>
  <header :class="$style.header">
    <h1 :class="$style.title">Добавление товара</h1>
    <button :class="$style.sortButton">
      <p :class="$style.text">По умолчанию</p>
    </button>
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

.sortButton {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 16px;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  background-color: $white;
  transition: $transition box-shadow;
  cursor: pointer;
  &:hover {
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.25);
  }
  @media (max-width: $container-small-size) {
    margin-top: 24px;
  }
}

.text {
  display: flex;
  align-items: center;
  font-size: 12px;
  line-height: 15px;
  color: $gray;
  &:after {
    content: '';
    display: block;
    width: 5px;
    height: 5px;
    margin-left: 5px;
    margin-bottom: 2.5px;
    border-bottom: 1px solid $gray;
    border-right: 1px solid $gray;
    transform: rotate(45deg);
  }
}
</style>
