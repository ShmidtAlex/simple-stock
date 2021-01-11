<template>
  <div class="review-tabs">
    <span class="tab"
    :class="{ activeTab: selectedTab === tab }" 
    v-for="(tab, index) in tabs" 
    :key="index"
    @click="selectedTab = tab"
    >{{ tab }}</span>
    
    <div class="review-wrapper">
      <div v-show="selectedTab === 'Reviews'" id="tab1">
        <div class="review-box">
          <h2>Reviews</h2>
          <div>
            <p v-show="!reviews.length">There are no reviews yet</p>
            <ul v-show="reviews.length" class="listed-review">
              <li class="review-item" v-for="(review, index) in reviews" :key="index">
                <ul class="stars-list">
                  <li class="star" v-for="(star, index) in review.rating" :key="index"></li>
                </ul>
                <i>{{review.review ? `\"${review.review}\"` : `I recommend this product: ${review.recommendation}` }}</i>
                <div class="name">{{review.name}}</div>
              </li>            
            </ul>
          </div>
        </div>
      </div>
      <div v-show="selectedTab === 'Make a Review' " id="tab2">
        <ProductReview @reviewSubmitted="showReview"/>
      </div>
    </div>
  </div>
</template>
<script>
  import ProductReview from './ProductReview.vue'
  export default {
    name: 'ReviewTabs',
    components: {
      ProductReview
    },
    data() {
      return {
        tabs: ['Reviews', 'Make a Review'],
        selectedTab: 'Reviews',
        reviews: []
      }
    },
    methods: {
      showReview(productReview) {
        this.reviews.push(productReview)
      }
    }
  }
</script>
<style>
  .review-tabs {
    display: flex;
    justify-content: flex-start;
    margin: 0 100px;
    position: relative;
  }
  .tab {
    margin: 0 1px;
    position: absolute;
    left: -1px;
    color: darkblue;
    font-weight: 600;
    border-top: 2px solid darkblue;
    border-left: 2px solid darkblue;
    border-right: 2px solid darkblue;
    padding: 0 10px;
    border-radius: 5px 5px 0 0;
    z-index: 2;
    width: 100px;
  }
  .tab:nth-child(2) {
    border-left: none;
    border-radius: 0 5px 0 0;
    left: 100px;
    min-width: fit-content;
  }
  .activeTab {
    font-weight: 800;
    color: blue;
    border: 2px solid blue;
    border-bottom: 2px solid whitesmoke;
    background-color: whitesmoke
  }
  #tab1, #tab2 {
    position: absolute;
    left: 0;
    top: 26px;
    border: 2px solid blue;
    border-radius: 0 5px;
    z-index: 1;
    background-color: whitesmoke;
  }
</style>
