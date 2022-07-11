<template>
  <div id="app" class="d-flex">
    <add-product @add-new-product="addNewProduct($event)"/>
    <the-products 
      :products="filteredProducts" 
      @delete-product="deleteProduct($event)"
      @option-change="optionChange($event)"
    />
  </div>
</template>

<script>
import AddProduct from './components/AddProduct/index.vue'
import TheProducts from './components/Products/index.vue'

export default {
  name: 'App',
  components: {
    AddProduct,
    TheProducts
  },
  mounted() {
    if (localStorage.getItem('products')) {
      try {
        this.products = JSON.parse(localStorage.getItem('products'));
      } catch(e) {
        console.log(e);
      }
    }
  },
  data() {
    return {
      products: [
        { id: 1, img: 'https://kartinkin.net/uploads/posts/2021-07/1625248984_16-kartinkin-com-p-fon-fotoapparat-krasivie-foni-16.jpg', name: 'АНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '10 000' },
        { id: 2, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ВНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '22 000' },
        { id: 3, img: 'https://phonoteka.org/uploads/posts/2021-04/1618592387_35-phonoteka_org-p-fon-dlya-fotografa-54.jpg', name: 'БНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '20 000' },
        { id: 4, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612495387_66-p-serii-fon-fotoapparat-113.jpg', name: 'ГНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '15 000' },
        { id: 5, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ДНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. ', price: '100 000' },
        { id: 3, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'БНаименование товара', text: 'Довольно-таки интересное', price: '20 000' },
        { id: 4, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ГНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '15 000' },
        { id: 5, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ДНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '100 000' },
        { id: 3, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'БНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '20 000' },
        { id: 4, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ГНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '15 000' },
        { id: 5, img: 'https://catherineasquithgallery.com/uploads/posts/2021-02/1612508280_7-p-kamera-na-serom-fone-8.jpg', name: 'ДНаименование товара', text: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк', price: '100 000' },
      ],
      optionIsActive: 1
    }
  },
  watch: {
    products: function() {
      let products = JSON.stringify(this.products)
      localStorage.setItem("products", products)
    },
  },
  computed: {
    filteredProducts: function() {
      if (this.optionIsActive === 2) { 
        return this.products.slice().sort(this.sortPriceMin) 
      }
      if (this.optionIsActive === 3) { 
        return this.products.slice().sort(this.sortPriceMax) 
      }
      if (this.optionIsActive === 4) { 
        return this.products.slice().sort(this.sortName) 
      }
      return this.products 
    }
  },
  methods: {
    addNewProduct(product) {
      this.products.push(product)
    },
    deleteProduct(id) {
      this.products = this.products.filter(el => el.id != id)
    },
    optionChange(option) {
      this.optionIsActive = option
    },
    sortName(x, y) {
      if (x.name < y.name) {return -1;}
      if (x.name > y.name) {return 1;}
      return 0;
    },
    sortPriceMin(x, y) {
      let a = +x.price.replace(/\s/g, '');
      let b = +y.price.replace(/\s/g, '');
      if (a < b) {return -1;}
      if (a > b) {return 1;}
      return 0;
    },
    sortPriceMax(x, y) {
      let a = +x.price.replace(/\s/g, '');
      let b = +y.price.replace(/\s/g, '');
      if (a > b) {return -1;}
      if (a < b) {return 1;}
      return 0;
    },
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/global.scss';

  #app {
    display: flex;
    align-items: stretch;

    @media screen and (max-width: 1024px) {
      flex-direction: column;
      align-items: center;
    }
  }
</style>
