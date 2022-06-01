<script>
export default {
  inheritAttrs: false,
  props: {
    label: String,
    modelValue: String | Number,
    required: Boolean,
    field: {
      default: 'input',
    },
  },
};
</script>
<template>
  <p :class="[$style.label, required ? $style.required : '']">{{ label }}</p>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    v-if="field === 'input'"
    v-bind="$attrs"
    type="text"
    :class="[
      $style.field,
      $style.inputField,
      !modelValue && modelValue !== null && required ? $style.error : '',
    ]"
  />
  <textarea
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    v-else-if="field === 'textarea'"
    v-bind="$attrs"
    :class="[$style.field, $style.textareaField]"
  />
  <p
    :class="[
      $style.errorMessage,
      !modelValue && modelValue !== null && required
        ? $style.showErrorMessage
        : '',
    ]"
  >
    Поле является обязательным
  </p>
</template>

<style module lang="scss">
@import '@/styles/vars.scss';
.field {
  width: 100%;
  padding: 10px 16px;
  margin-top: 4px;
  outline: 1px solid transparent;
  border: none;
  border-radius: 4px;
  background: $white;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  font-size: 12px;
  line-height: 15px;
  color: $black;
  transition: $transition box-shadow, $transition outline;
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
  position: relative;
  width: fit-content;
  font-size: 10px;
  line-height: 13px;
  color: #49485e;
}

.required {
  &::before {
    content: '';
    position: absolute;
    top: 0;
    right: -4px;
    display: block;
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background-color: #ff8484;
  }
}

.error {
  position: relative;
  outline: 1px solid #ff8484;
  transition: $transition outline;
}

.errorMessage {
  opacity: 0;
  margin-top: 4px;
  font-size: 8px;
  line-height: 10px;
  color: #ff8484;
  transition: $transition opacity;
}

.showErrorMessage {
  opacity: 1;
}
</style>
