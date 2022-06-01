<script>
export default {
  inheritAttrs: false,
  props: {
    label: String,
    field: {
      default: 'input',
    },
  },
};
</script>
<template>
  <p :class="$style.label">{{ label }}</p>
  <input
    v-if="field === 'input'"
    v-bind="$attrs"
    type="text"
    :class="[$style.field, $style.inputField]"
  />
  <textarea
    v-else-if="field === 'textarea'"
    v-bind="$attrs"
    :class="[$style.field, $style.textareaField]"
  />
</template>

<style module lang="scss">
@import '@/styles/vars.scss';
.field {
  width: 100%;
  padding: 10px 16px;
  margin-top: 4px;
  outline: none;
  border: none;
  border-radius: 4px;
  background: $white;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: $transition box-shadow;
  font-size: 12px;
  line-height: 15px;
  color: $black;
  &:focus {
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.25);
  }
  &::placeholder {
    color: #b4b4b4;
  }
}

.textareaField {
  height: 108px;
  resize: none;
}

.label {
  font-size: 10px;
  line-height: 13px;
  color: #49485e;
}
</style>
