<template>
 <div class="product">
  <div class="product-image">
    <img :src="image" alt="green socks picture">
  </div>
  <div class="product-info">
    <h1>{{ product }}</h1>
    <h2>{{ description }}</h2>
    <h2 :class="{ crossedOut: !computedInStock}">In Stock</h2>

    <Details :details="details" />
    
    <div class="variants" >
      <p @mouseover="updateColor(index)" v-for="(variant, index) in variants"
      :key="variant.variantId"
      class="color-box btn"
      :style="{ backgroundColor: variant.variantColor }"
      >{{ variant.variantColor === '#ffd800' ? 'yellow' : 'green' }}</p>
    </div>
    <div class="sizes" >
      <p  v-for="(size, index) in sizes" :key="index">{{ size }}</p>
    </div>
    <div class="cart-block">
      <AddButton :name="addName" @changeItemNumber="addToCart" :availability="computedInStock"/>
      <button class="btn btn-warning" 
        @click="deleteFromCart"
        :disabled="!computedInCart" 
        >Decrease Amount of items</button>
    </div>
     
  </div> 
 </div>
</template>

<script>
  import AddButton from './AddButton.vue'
  import Details from './Details.vue'
export default {
  name: 'Socks',
  components: {
    AddButton,
    Details
  },
  props: {
    cartState: {
      type: Boolean,
      require: true
    }
  },
  data() {
    return {
      product: 'Socks',
      description: 'it is a very good socks for winter sports',
      // image: require('../assets/plain-green-socks.jpg'),
      selectedVariant: 0,
      inStock: true,
      inventory: 7,
      details: [ '80% cotton', '20% polyester', 'Gender-newtral'],
      sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL'],
      variants: [
        { variantId: 234,
          variantColor: "green",
          variantImage: require('../assets/plain-green-socks.jpg'),
          quantity: 0
        },
        { variantId: 235,
          variantColor: "#ffd800",
          variantImage: require('../assets/yellow-new-york-cab-socks2x.jpg'),
          quantity: 7
        }
      ],
      addName: 'Add to cart',
    }
  },
  methods: {
    addToCart() {
      if(this.computedInStock) {
        this.variants[this.selectedVariant].quantity--
        this.$emit('decreaseItemNumber', this.variants[this.selectedVariant].variantId)
      } else {
        alert('Sorry, this item is unavailable anymore')
      }
      
    },
    deleteFromCart() {      
      this.$emit('deleteItemFromCart', this.variants[this.selectedVariant].variantId)     
    },
    updateColor(image) {      
      this.selectedVariant = image
    }
  },
  computed: {
    computedInStock() {
      return this.variants[this.selectedVariant].quantity > 0
    },
    computedInCart() {
      return this.cartState
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    }
  }
  
}
</script>
<style scoped lang="scss">
  .product {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
  }
  .product-image, .product-info {
    width: 30%;
    height: 300px;    
    display: flex;
    justify-content: center;
    align-items: center;
    // border: 1px solid green;
    img {
      width: 75%;
      height: 100%
    }
  }
  .product-image {
    width: 550px;
  }
  .product-info {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding-left: 50px;
  }
  
  li {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
  }
  .variants p {
    // border: 1px solid grey;
    padding: 0;
    margin: 15px 0;
    font-weight: 600;
    font-size: 18px;
  }
  .color-box {
    margin: 5px;
    padding: 10px;
    width: 100px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .sizes {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .cart-block {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    width: 100%;
  }
  h2 {
    text-align: left;
  }
  .crossedOut {
    text-decoration: line-through;
  }

</style>
