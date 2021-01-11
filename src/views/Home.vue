<template>
  <div class="home">
    
    <div class="socks-wrapper">      
      <Socks 
        @decreaseItemNumber="addToCart" 
        :cartState="cart.length > 0"
        @deleteItemFromCart="removeFromCart"
        />
      <div class="cart-block">        
        <p class="cart">Cart {{ cart.length }}</p>        
      </div>
    </div>    
     <ReviewTabs />   
  </div>
</template>

<script>
import Socks from '@/components/Socks.vue'
// import ProductReview from '@/components/ProductReview.vue'
import ReviewTabs from '@/components/ReviewTabs.vue'
export default {
  name: 'App',
  components: {
    Socks,
    // ProductReview,
    ReviewTabs
  },
  data() {
    return {
      cart: []
    }
  },
  methods: {
    addToCart(value) {
      this.cart.push(value);
    },
    removeFromCart(value) {
      if (this.cart.length > 0) {
        this.cart.splice(this.cart.indexOf(value), 1);
      } 
    },
    
  }
}
</script>
<style lang="scss">
.home {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  display: flex;
  flex-direction: column;
  margin-top: 27px;
  .nav-bar {
    height: 50px;
    background: linear-gradient(to right, #2C7516, #38B712, #43D218);
  }
  .socks-wrapper {
    height: 60%;
    display: flex;
  }
  .review-wrapper{
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
  }
 
  .review-box {
    width: 50%;
    margin: 30px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
   .listed-review {
    display: flex;
    flex-direction: row;
    margin: 0;
  }
  .cart-block {
    margin: 20px;
  }
  .cart {
    border: 1px solid grey;
    padding: 20px;
    float: right;
  }
  .review-item {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    width: 300px;
    background-color: whitesmoke; 
    margin: 2px;
    border-radius: 5px;
    i {
      font-size: 22px;
      width: 100%;
    }
    .name {
      font-size: 16px;
      width: 100%;
      display: flex;
      justify-content: flex-end;
      align-items: flex-end;
      padding: 0 40px;
      font-weight: 600;
    }
  }
  .stars-list {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    padding: 0;
  }
  .star { 
    width: 25px;
    height: 25px;
    background-image: url('../assets/Orange_star.svg');
    background-size: contain;
  }
  li {
    list-style-type: none;
  }
}
</style>
