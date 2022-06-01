<script>
import Input from '@/components/Input.vue';
export default {
  emits: ['addProduct'],
  data() {
    return {
      inputs: [
        {
          field: 'input',
          label: 'Наименование товара',
          placeholder: 'Введите наименование товара',
          key: 'name',
          value: null,
          required: true,
        },
        {
          field: 'textarea',
          label: 'Описание товара',
          placeholder: 'Введите описание товара',
          key: 'description',
          value: null,
          required: false,
        },
        {
          field: 'input',
          label: 'Ссылка на изображение товара',
          placeholder: 'Введите ссылку',
          key: 'image',
          value: null,
          required: true,
        },
        {
          field: 'input',
          label: 'Цена товара',
          placeholder: 'Введите цену',
          key: 'price',
          value: null,
          required: true,
        },
      ],
      showForm: false,
    };
  },
  components: {
    Input,
  },
  methods: {
    addThousandsSeparator(number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
    toggleForm() {
      this.showForm = !this.showForm;
    },
    addProduct() {
      const product = this.inputs.reduce((acc, val) => {
        return {
          ...acc,
          [val.key]: val.value,
        };
      }, {});
      this.showForm = false;
      this.inputs.map((item) => (item.value = ''));
      this.$emit('addProduct', product);
    },
    maskForPrice(input, value) {
      if (input.key === 'price') {
        const reg = /[A-zА-я]/g;
        const validateValue = value.split(' ').join('').replace(reg, '');
        return this.addThousandsSeparator(validateValue);
      } else {
        return value;
      }
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
  computed: {
    disabledButton() {
      for (let i = 0; i < this.inputs.length; i++) {
        const { value, required } = this.inputs[i];
        if (!value && required) {
          return true;
        }
      }
      return false;
    },
  },
};
</script>
<template>
  <div :class="[$style.form, !showForm ? $style.hideForm : '']">
    <div :class="$style.inputs">
      <div v-for="input in inputs" :key="input.label" :class="$style.input">
        <Input
          type="number"
          :modelValue="input.value"
          @update:modelValue="
            (newValue) => (input.value = maskForPrice(input, newValue))
          "
          :field="input.field"
          :label="input.label"
          :placeholder="input.placeholder"
          :required="input.required"
        />
      </div>
    </div>
    <div :class="$style.buttons">
      <button
        :class="$style.button"
        @click="addProduct"
        :disabled="disabledButton"
      >
        Добавить товар
      </button>
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
    margin-top: 2px;
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
    cursor: auto;
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
