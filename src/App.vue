<template>
  <div style="max-width:1200px; margin: auto;">
    <button type="button" class="create-button" @click="showModal">
      Создать товар
    </button>
    <div class="row">
      <ProductCard v-for="(product,id) in products" :key="id" :product="product" />
    </div>
  </div>
  <Modal v-show="isModalVisible" @close="closeModal" />
</template>

<script>
  import ProductCard from './components/ProductCard.vue'
  import Modal from './components/Modal.vue'
  import AXIOS from '@/plugins/axios'
  export default {
    name: 'App',
    data() {
      return {
        isModalVisible: false,
        products: []
      }
    },
    components: {
      ProductCard,
      Modal
    },
    beforeMount() {
      AXIOS.get('products').then((response) => {
        this.products = response.data
      }).catch(e => console.log("Не удалось загрузить товары\n" + e.message))
    },
    methods: {
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
      }
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans", sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    text-align: left;
    background-color: #fff;
  }

  .row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15 px;
    margin-left: -15 px;
  }
  .create-button{
    padding: 10px 20px;
    background-color: #0bf85a;
    font-weight: 600;
  }
</style>