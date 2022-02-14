<template>
  <div class="wrapper">
    <div class="header">
      <span class="add-product-text">Добавление товара</span>
      <button>По умолчанию</button>
    </div>
    <div class="container">
      <div class="add_product">
        <form class="form">
          <div>
            <span class="label_input">Наименование товара</span>
            <input />
          </div>
          <div>
            <span class="label_input">Описание товара</span>
            <input />
          </div>
          <div>
            <span class="label_input">Ссылка на изображение товара</span>
            <input />
          </div>
          <div>
            <span class="label_input">Цена товара</span>
            <input />
          </div>
          <button type="submit" class="btn_add_product">Добавить товар</button>
        </form>
      </div>
      <div class="list_products">
        list products
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App'

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
    height: 440px;

    padding: 24px;

    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
  }

  .label_input {
    font-size: 10px;
    color: #49485E;
    font-weight: normal;
  }
  .btn_add_product {
    background: #EEEEEE;
    border-radius: 10px;
    outline: none;
    width: 100%;
    border: none;
    cursor: pointer;

    padding: 10px 0;


    /* style for text */
    font-weight: 600;
    font-size: 12px;
    color: #B4B4B4;
  }

  .list_products {
    width: 1028px;
    height: auto;
  }
</style>
