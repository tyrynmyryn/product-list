<script>
export default {
  props: ['sortValues'],
  emits: ['sort'],
  data() {
    return {
      currentSort: 'По умолчанию',
      isOpen: false,
    };
  },
  methods: {
    handlePopup() {
      this.isOpen = !this.isOpen;
    },
    chooseSortMethod(method) {
      this.isOpen = false;
      this.currentSort = method;
      this.$emit('sort', this.currentSort);
    },
  },
};
</script>
<template>
  <div :class="$style.sort">
    <button :class="$style.sortButton" @click="handlePopup">
      <p :class="[$style.sortValue, isOpen ? $style.open : '']">
        {{ currentSort }}
      </p>
    </button>
    <ul :class="[$style.popup, isOpen ? $style.showPopup : '']">
      <li
        v-for="item in sortValues"
        :key="item"
        @click="() => chooseSortMethod(item)"
        :class="$style.item"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<style module lang="scss">
@import '../styles/vars.scss';

.sort {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
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

.sortValue {
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
    transition: $transition transform;
  }
}

.popup {
  opacity: 0;
  position: absolute;
  top: 100%;
  width: 100%;
  background: #fff;
  border-radius: 0 0 8px 8px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: $transition opacity;
  pointer-events: none;
  z-index: 100;
}

.open {
  &::after {
    margin-bottom: 0;
    margin-top: 2.5px;
    transform: rotate(-45deg) scale(1, -1);
  }
}

.showPopup {
  opacity: 1;
  pointer-events: all;
}

.item {
  padding: 12px 0;
  font-size: 12px;
  line-height: 15px;
  color: $gray;
  text-align: center;
  transition: $transition background-color;
  &:hover {
    background-color: $gray;
    color: #ffffff;
  }
  cursor: pointer;
  &:last-child {
    border-radius: 0 0 8px 8px;
  }
}
</style>
