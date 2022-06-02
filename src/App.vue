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
      sortValues: [
        'По умолчанию',
        'По цене min',
        'По цене max',
        'По наименованию',
      ],
      currentSortMethod: 'По умолчанию',
    };
  },
  methods: {
    fetchData(total) {
      const product = {
        id: null,
        name: 'Наименование товара',
        description:
          'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: 10000,
        image: img,
      };
      const productArray = [];
      for (let i = 0; i < total; i++) {
        productArray.push({ ...product, id: i });
      }
      return productArray;
    },
    addProduct(product) {
      this.data.push({ ...product, id: Date.now() });
      window.localStorage.setItem('data', JSON.stringify(this.data));
    },
    deleteProduct(product) {
      this.data = this.data.filter((item) => item.id !== product.id);
      window.localStorage.setItem('data', JSON.stringify(this.data));
    },
    sort(method) {
      this.currentSortMethod = method;
    },
    priceToInt(price) {
      return parseInt(price.toString().split(' ').join(''), 10);
    },
  },
  computed: {
    sortedArray() {
      switch (this.currentSortMethod) {
        case 'По цене min':
          return this.data.sort((a, b) =>
            this.priceToInt(a.price) > this.priceToInt(b.price) ? 1 : -1
          );
        case 'По цене max':
          return this.data.sort((a, b) =>
            this.priceToInt(a.price) < this.priceToInt(b.price) ? 1 : -1
          );
        case 'По наименованию':
          return this.data.sort((a, b) =>
            a.name.toLowerCase() > b.name.toLowerCase() ? 1 : -1
          );
        default:
          this.data = JSON.parse(window.localStorage.getItem('data'));
          return this.data;
      }
    },
  },
  created() {
    if (!window.localStorage.getItem('data')) {
      window.localStorage.setItem('data', JSON.stringify(this.fetchData(3)));
    }
    this.data = JSON.parse(window.localStorage.getItem('data'));
  },
};
</script>

<template>
  <Layout>
    <Header :sort="sort" :sortValues="sortValues" />
    <AddForm @addProduct="addProduct" />
    <Products :products="sortedArray" @deleteProduct="deleteProduct" />
  </Layout>
</template>

<style module lang="scss">
@import '@/styles/main.scss';
</style>
