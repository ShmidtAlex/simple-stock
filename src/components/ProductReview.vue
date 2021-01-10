<template>
  <div class="product-review">
    <form class=" form-group" @submit.prevent="onSubmit">
      <p>
        <label for="name">Name:</label>
        <input class="form-control" type="text" id="name" v-model="name" required="">
      </p>
      <p>
        <label for="review">Review:</label>
        <textarea class="form-control" name="" id="review" v-model="review" cols="30" rows="5"></textarea>
      </p>
      <p>
        <label for="rating">Rating:</label>
        <select class="form-control" name="" id="rating" v-model.number="rating" required="">
          <option value="5">5</option>
          <option value="4">4</option>
          <option value="3">3</option>
          <option value="2">2</option>
          <option value="1">1</option>
        </select>
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
        rating: null
      }
    },
    methods: {
      onSubmit() {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating
        }
        this.$emit('reviewSubmitted', productReview)
        this.name = null
        this.review = null
        this.rating = null
      }
    }
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
  }
</style>