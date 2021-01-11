<template>
  <div class="product-review">
    <form class=" form-group" @submit.prevent="onSubmit">
      <p class="errors" v-if="errors.length">
        <span>Please, correct the following error(s):</span>
        <span class="error" v-for="(error, index) in errors" :key="index">{{ error }} </span>
      </p>
      <p>
        <label for="name">Name:</label>
        <input class="form-control" type="text" id="name" v-model="name">
      </p>
      <p>
        <label for="review">Review:</label>
        <textarea class="form-control" name="" id="review" v-model="review" cols="30" rows="5"></textarea>
      </p>
      <p>
        <label for="rating">Rating:</label>
        <select class="form-control" name="" id="rating" v-model.number="rating">
          <option value="5">5</option>
          <option value="4">4</option>
          <option value="3">3</option>
          <option value="2">2</option>
          <option value="1">1</option>
        </select>
      </p>
      
      <p>
        <label for="">Would you recommend this product?</label><br>

        <input id="yesAnswer" name="recommendation" type="radio" checked @input="getRecommendation" value="yes">
        <label for="yesAnswer" > Yes</label><br>
        <input id="noAnswer" name="recommendation" type="radio" @input="getRecommendation" value="no">
        <label for="noAnswer"> No</label>
      </p>      
      <p>
        <input type="submit" value="Submit">
      </p>
    </form>
    
  </div>
</template>
<script>
  export default {
    data() {
      return {
        name: null,
        review: null,
        rating: null,
        recommendation: 'yes',
        errors: []
      }
    },
    methods: {
      onSubmit() {
        if(this.name && this.rating) {
          let productReview = {
            name: this.name,
            review: this.review,
            rating: this.rating,
            recommendation: this.recommendation
          }
          this.$emit('reviewSubmitted', productReview)
          this.name = null
          this.review = null
          this.rating = null
          this.errors = []
          this.recommendation = "yes"
        } else {
          if(!this.name) {
            this.errors.push("Name required")
          }
          if (!this.rating) {
            this.errors.push("Rating required")
          }
        }
        
      },
      getRecommendation(){
        this.recommendation = event.target.value;
        console.log(this.recommendation)
      }
    },

  }
  
</script>
<style>
  .product-review {    
    margin: 30px 100px;
    padding: 30px 100px;
  }.
  .review-form {
    display: flex;
    flex-direction: row;
    position: relative;
  }
  .errors {
    display: flex;
    flex-direction: column;
    color: red;
    position: absolute;
    right: -20px;
    background-color: whitesmoke;
    border-radius: 5px;
    padding: 20px;
  }
</style>