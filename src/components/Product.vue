<template>
    <div class="product" v-for="product in products" :key="product.id">
        <img class="product_img" :src="product.linkProductImage" alt=""/>
        <div class="product_info">
            <p>{{ product.productName }}</p>
            <p>{{ product.descriptionProduct }}</p>
            <p>{{ product.priceProduct }} руб.</p>
        </div>
        <span class="btn_delete" @click="$emit('onRemoveProduct', product.id)">
            <img src="../assets/bin.png" alt="delete">
        </span>
     </div>
</template>

<script>
export default {
    props: {
        products: {
            type: Array,
            default: () => []
        }
    }
}
</script>

<style scoped>


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
</style>