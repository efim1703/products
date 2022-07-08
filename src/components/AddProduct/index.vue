<template>
  <div class="add-product">
    <h2>Добавление товара</h2>

    <div class="add-form">
      <c-input 
        nameInput="Наименование товара" 
        :isRequired="true" 
        placeholder="Введите наименование товара"
        @input="nameProduct = $event"
        :value="nameProduct"
        :error="errors.name"
      />
      <c-textarea 
        nameTextarea="Описание товара" 
        placeholder="Введите описание товара"
        @input="aboutProduct = $event"
        :value="aboutProduct"
      />
      <c-input 
        nameInput="Ссылка на изображение товара"
        :isRequired="true" 
        placeholder="Введите ссылку"
        @input="linkProduct = $event"
        :value="linkProduct"
        :error="errors.link"
      />
      <input-number
        nameInput="Цена товара" 
        :isRequired="true"
        placeholder="Введите цену"
        @input="priceProduct = $event"
        :value="priceProduct"
        :error="errors.price"
      />

      <c-btn @click="addProduct()" :isDisabled="btnIsDisabled">Добавить товар</c-btn>
    </div>
  </div>
</template>

<script>
import CInput from './CInput.vue'
import CTextarea from './CTextarea.vue'
import InputNumber from './InputNumber.vue'
import CBtn from './CBtn.vue'

export default {
  name: 'AddProduct',
  components: {
    CInput,
    CTextarea,
    InputNumber,
    CBtn
  },
  data() {
    return {
      nameProduct: '',
      aboutProduct: '',
      linkProduct: '',
      priceProduct: 0,
      errors: {
        name: '',
        link: '',
        price: ''
      }
    }
  },
  watch: {
    nameProduct: function() {
      this.nameProduct == '' ? this.errors.name = 'Поле является обязательным' : this.errors.name = ''
    },
    linkProduct: function() {
      this.linkProduct == '' ? this.errors.link = 'Поле является обязательным' : this.errors.link = ''
    },
    priceProduct: function() {
      this.priceProduct == 0 ? this.errors.price = 'Поле является обязательным' : this.errors.price = ''
    }
    
  },
  methods: {
    addProduct() {
      let id = new Date().getTime()
      let newProduct = {
        id: id,
        img: this.linkProduct,
        name: this.nameProduct,
        text: this.aboutProduct,
        price: this.priceProduct.toLocaleString()
      }
      this.$emit('add-new-product', newProduct)
    },
    
  },
  computed: {
    btnIsDisabled() {
      return !!(!this.nameProduct || !this.priceProduct || !this.linkProduct)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';

  .add-product {
    position: relative;
    max-width: 332px;
    width: 100%;
    min-height: 100%;
    margin-right: 16px;
  }
  h2 {
    height: 36px;
    font-weight: 600;
    font-size: 28px;
    padding-top: 32px;
    margin-bottom: 16px;

    @media screen and (max-width: 425px) {
      font-size: 22px;
    }
  }
  .add-form {
    position: sticky;
    top: 24px;
    display: flex;
    flex-direction: column;
    padding: 24px;
    background: $white;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    @media screen and (max-width: 1024px) {
      text-align: center;
      max-width: 80%;
    }
  }
</style>