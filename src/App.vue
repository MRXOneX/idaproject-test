<template>
  <div class="wrapper">
    <div class="header">
      <span class="add-product-text">Добавление товара</span>
      <select-sort />
    </div>
    <div class="container">
      <div>
        <div class="add_product">
          <form-product @onAddProduct="addProduct"/>
        </div>
      </div>
      <div class="list_products">
        <product @onRemoveProduct="removeProduct" :products="products"/>
      </div>
    </div>
  </div>
</template>

<script>
// components
import FormProduct from './components/FormProduct.vue'
import Product from './components/Product.vue'
import SelectSort from './components/SelectSort.vue'

export default {
  name: 'App',
  components: { FormProduct, Product, SelectSort },

  

  data() {
    return {
      products: JSON.parse(localStorage.getItem('products'))
    }
  },

  methods: {
    removeProduct(id) {
      console.log(id)
      const products = JSON.parse(localStorage.getItem('products'))

      const newProducts = products.filter(product => product.id !== id)
      this.products = newProducts

      localStorage.setItem('products', JSON.stringify(newProducts))
    },
    onAddProduct(product) {
      const previosProducts = JSON.parse(localStorage.getItem('products')) || []
      const currentProducts = [...previosProducts, {id: uniqid('', '-product'),...product}]

      localStorage.setItem('products', JSON.stringify(currentProducts))
      this.products = currentProducts
    }
  }

}
</script>

<style>
  /* fonts */
  @import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,200;0,300;0,400;0,600;1,200;1,300;1,400;1,600&display=swap');
  /* ----- */


  body {
    margin: 0;
    padding: 0;
    height: 100%;
    box-sizing: border-box;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background: rgba(255, 254, 251, 0.8);

    height: 100%;
  }


  .wrapper {
    padding: 32px;
  }

  .add-product-text {
    font-family: 'Source Sans Pro', sans-serif;
    font-style: normal;
    font-weight: 600;
    font-size: 28px;
    color: #3F3F3F;
  }



  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .container {
    display: flex;
    flex-direction: row;
    margin: 16px 0 0 0;
  }


  .add_product {
    width: 332px;
    height: auto;

    padding: 24px;

    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
  }


  .list_products {
    width: 1028px;
    height: auto;

    margin: 0 0 0 16px;

    display: grid; 
    grid-auto-columns: 1fr; 
    grid-template-columns: 1fr 1fr 1fr; 
    gap: 21px 21px; 
  }

</style>
