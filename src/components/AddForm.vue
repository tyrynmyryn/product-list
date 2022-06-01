<script>
import Input from '@/components/Input.vue';
export default {
  data() {
    return {
      inputs: [
        {
          field: 'input',
          label: 'Наименование товара',
          placeholder: 'Введите наименование товара',
        },
        {
          field: 'textarea',
          label: 'Описание товара',
          placeholder: 'Введите описание товара',
        },
        {
          field: 'input',
          label: 'Ссылка на изображение товара',
          placeholder: 'Введите ссылку',
        },
        { field: 'input', label: 'Цена товара', placeholder: 'Введите цену' },
      ],
      showForm: false,
    };
  },
  components: {
    Input,
  },
  methods: {
    toggleForm() {
      this.showForm = !this.showForm;
    },
  },
  watch: {
    showForm(isOpen) {
      if (isOpen) {
        document.body.style.overflow = 'hidden';
      } else {
        document.body.style.overflow = 'auto';
      }
    },
  },
};
</script>
<template>
  <div :class="[$style.form, !showForm ? $style.hideForm : '']">
    <div :class="$style.inputs">
      <div v-for="input in inputs" :key="input.label" :class="$style.input">
        <Input
          :field="input.field"
          :label="input.label"
          :placeholder="input.placeholder"
        />
      </div>
    </div>
    <div :class="$style.buttons">
      <button :class="$style.button">Добавить товар</button>
      <button :class="[$style.button, $style.backButton]" @click="toggleForm">
        Назад
      </button>
    </div>
  </div>
  <button :class="[$style.button, $style.showFormButton]" @click="toggleForm">
    Добавить товар
  </button>
</template>

<style module lang="scss">
@import '@/styles/vars.scss';
.form {
  position: sticky;
  top: 24px;
  left: 0;
  grid-column: 1 / 5;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: fit-content;
  padding: 24px;
  border-radius: 4px;
  background-color: $white;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  @media (max-width: $container-medium-size) {
    grid-column: 1 / 7;
  }
  @media (max-width: $container-small-size) {
    grid-column: 1 / -1;
    position: absolute;
    top: 0;
    left: 0;
    height: 100vh;
    justify-content: space-between;
    background-color: rgba($white, 0.95);
    z-index: 100;
  }
}

.hideForm {
  @media (max-width: $container-small-size) {
    display: none;
  }
}

.input {
  &:not(:first-child) {
    margin-top: 16px;
  }
}

.buttons {
  display: flex;
}

.button {
  width: 100%;
  padding: 10px 20px;
  margin-top: 24px;
  border: none;
  border-radius: 10px;
  background-color: #7bae73;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 12px;
  font-weight: 600;
  line-height: 15px;
  color: #ffffff;
  transition: $transition background-color;
  cursor: pointer;
  &:hover {
    background-color: darken(#7bae73, 12%);
  }
  &:active {
    background-color: darken(#7bae73, 8%);
  }
  &:disabled {
    background-color: #eeeeee;
    color: $gray;
  }
  @media (max-width: $container-small-size) {
    justify-self: end;
  }
}

.showFormButton {
  display: none;
  @media (max-width: $container-small-size) {
    display: block;
    grid-column: 1 / -1;
    margin-top: 0;
    margin-bottom: 10px;
  }
}

.backButton {
  display: none;
  background-color: #ae7373;
  &:hover {
    background-color: darken(#ae7373, 12%);
  }
  &:active {
    background-color: darken(#ae7373, 8%);
  }
  @media (max-width: $container-small-size) {
    display: block;
    margin-left: 24px;
  }
}
</style>
