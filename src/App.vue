<template>
  <div class="wrapper">
    <div class="header">
      <span class="add-product-text">Добавление товара</span>
      <select class="select-sort">
        <option default>От меньшего к большему</option>
        <option>От большего к меньшему</option>
        <option>По наименованию</option>
      </select>
    </div>
    <div class="container">
      <div>
        <div class="add_product">
          <form class="form" @submit.prevent="addProduct">

            <div>
              <p class="label_input">Наименование товара</p>
              <input 
                :class="v$.form.productName.$error ? 'error' : ''" 
                v-model="form.productName" 
                placeholder="Введите наименование товара" 
                class="input"
              />
            </div>
            <p class="error-text" v-for="(error, index) of v$.form.productName.$errors" :key="index">
              {{ error.$message }}
            </p>


            <div>
              <p class="label_input">Описание товара</p>
              <textarea v-model="form.descriptionProduct" placeholder="Введите описание товара" class="input textarea"/>
            </div>


            <div>
              <p class="label_input">Ссылка на изображение товара</p>
              <input 
                :class="v$.form.linkProductImage.$error ? 'error' : ''" 
                v-model="form.linkProductImage" 
                placeholder="Введите ссылку" 
                class="input"
              />
            </div>
            <p class="error-text" v-for="(error, index) of v$.form.linkProductImage.$errors" :key="index">
              {{ error.$message }}
            </p>


            <div>
              <p class="label_input">Цена товара</p>
              <input 
                :class="v$.form.priceProduct.$error ? 'error' : ''" 
                type="number" 
                v-model="form.priceProduct" 
                placeholder="Введите цену" 
                class="input"
              />
            </div>
            <p class="error-text" v-for="(error, index) of v$.form.priceProduct.$errors" :key="index">
              {{ error.$message }}
            </p>


            <button 
              type="submit" 
              class="btn_add_product"
              :class="this.v$.form.$error ? 'btn_add_product_disabled' : 'btn_add_product_active'"
              :disabled="this.v$.form.$error"
            >
              Добавить товар
            </button>
          </form>
        </div>
      </div>
      <div class="list_products">
        <div class="product" v-for="product in products" :key="product.id">
          <img class="product_img" :src="product.linkProductImage" alt=""/>
          <div class="product_info">
            <p>{{ product.productName }}</p>
            <p>{{ product.descriptionProduct }}</p>
            <p>{{ product.priceProduct }} руб.</p>
          </div>
          <span class="btn_delete" @click="removeProduct(product.id)">
            <img src="./assets/bin.png" alt="delete">
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import uniqid from 'uniqid';
//
import useVuelidate from "@vuelidate/core";
import { required, helpers  } from "@vuelidate/validators";

export default {
  name: 'App',

  

  data() {
    return {
      v$: useVuelidate(),
      form: {
        productName: '',
        descriptionProduct: '',
        linkProductImage: '',
        priceProduct: '',
      },
      products: JSON.parse(localStorage.getItem('products'))
    }
  },

  validations() {
    return {
      form: {
        productName: { required: helpers.withMessage('Поле является обязательным', required)},
        linkProductImage: { required: helpers.withMessage('Поле является обязательным', required)},
        priceProduct: { required: helpers.withMessage('Поле является обязательным', required)}
      }
    }
  },


  methods: {
    addProduct() {
      this.v$.form.$touch()
      if (!this.v$.form.$error) {
        const previosProducts = JSON.parse(localStorage.getItem('products')) || []

        const currentProducts = [...previosProducts, {id: uniqid('', '-product'),...this.form}]

        localStorage.setItem('products', JSON.stringify(currentProducts))
        this.products = currentProducts
      }
    },

    removeProduct(id) {
      const products = JSON.parse(localStorage.getItem('products'))

      const newProducts = products.filter(product => product.id !== id)
      this.products = newProducts

      localStorage.setItem('products', JSON.stringify(newProducts))
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

  .select-sort {
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    border: none;
    outline: none;
    cursor: pointer;

    /* style for text */
    font-weight: normal;
    font-size: 12px;
    color: #B4B4B4;
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


  .label_input {
    font-size: 10px;
    color: #49485E;
    font-weight: normal;

    margin: 16px 0;
  }
  .input {
    width: 100%;
    outline: none;
    border: none;
    padding: 10px 16px;

    color: #B4B4B4;
    font-weight: normal;
    font-size: 12px;
    background: #FFFEFB;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    box-sizing: border-box;
  }

  .textarea {
    height: 108px;
    resize: none;
  }



  .btn_add_product {
    border-radius: 10px;
    outline: none;
    width: 100%;
    border: none;
    cursor: pointer;
    margin: 24px 0 0 0;

    padding: 10px 0;


    /* style for text */
    font-weight: 600;
    font-size: 12px;
    color: #B4B4B4;
  }

  .btn_add_product_active {
    background: #7BAE73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    color: #FFFFFF;
  }
  .btn_add_product_disabled {
    background: #EEEEEE;
    color: #B4B4B4;
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

  .product {
    width: 332px;
    height: 423px;

    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    display: flex;
    flex-direction: column;

    position: relative;
  }

  .product_img {
    width: 100%;
    height: 200px;
    border-radius: 4px 4px 0 0;
  }

  .product_info {
    padding: 16px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
  }
  .product_info p {
    margin: 0;
    color: #3F3F3F;
  }

  .product_info p:nth-child(1) {
    font-weight: 600;
    font-size: 20px;
  }
  .product_info p:nth-child(2) {
    font-weight: normal;
    font-size: 16px;
  }
  .product_info p:nth-child(3) {
    font-weight: 600;
    font-size: 24px;
  }

  .btn_delete {
    position: absolute;
    right: -10px;
    top: -10px;

    background: #FF8484;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    padding: 8px;
    border: none;
    outline: none;
    cursor: pointer;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  .btn_delete img {
    height: 15px;
    width: 15px;
  }



    /* S T Y L E   F O R   V A L I D A T I O N */
    
    .error {
        border: 1px solid red;
    }
    .error::placeholder {
        color: red;
    }
    .error-text {
        color: red;
        margin: 3px;
        padding: 0;
        font-size: 10px;
    }
</style>
