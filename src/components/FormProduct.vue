<template>
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
</template>


<script>
import useVuelidate from "@vuelidate/core";
import { required, helpers  } from "@vuelidate/validators";
//
import uniqid from 'uniqid';


export default {
    data() {
        return {
            v$: useVuelidate(),
            form: {
                productName: '',
                descriptionProduct: '',
                linkProductImage: '',
                priceProduct: '',
            },
        }
    },
    methods: {
        addProduct() {
            this.v$.form.$touch()
            if (!this.v$.form.$error) {
                this.$emit('addProduct', this.form)
            }
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
}
</script>

<style scoped>


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