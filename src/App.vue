<script>
import Layout from '@/components/Layout.vue';
import Header from '@/components/Header.vue';
import AddForm from '@/components/AddForm.vue';
import Products from '@/components/Products.vue';
import img from '@/assets/img/product.png';

export default {
  components: {
    Layout,
    Header,
    AddForm,
    Products,
  },
  data() {
    return {
      data: [],
    };
  },
  methods: {
    fetchData(total) {
      const product = {
        name: 'Наименование товара',
        description:
          'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10000,
        image: img,
      };
      for (let i = 0; i < total; i++) {
        this.data.push(product);
      }
    },
    addProduct(product) {
      this.data.push(product);
    },
  },
  created() {
    this.fetchData(3);
  },
};
</script>

<template>
  <Layout>
    <Header />
    <AddForm @addProduct="addProduct" />
    <Products :products="data" />
  </Layout>
</template>

<style module lang="scss">
@import '@/styles/main.scss';
</style>
