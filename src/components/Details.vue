<template>
  <div class="details-wrapper">
    <h3>Details:</h3>
    <ul class="details-list">
      <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
    </ul>
  </div>  
</template>
<script>
  export default {
    name: 'Details',
    props: {
      details: {
        type: Array,
        require: true
      }
    }
  }
</script>
<style>
  .details-list {
    list-style-type: none;    
    padding: 0 0 0 20px;
    margin: 0;
    text-align: left;
  }
</style>