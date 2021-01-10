<template>
  <div>
    <button class="btn btn-primary" @click="add" :disabled="!availability">{{ name }}</button>
  </div>
</template>
<script>
  export default {
    name: 'AddToCart',
    props: {
      name: {
        type: String,
        require: true
      },
      availability: {
        type: Boolean,
        require: false
      }
    },
    data() {
      return {

      }
    },
    methods: {
      add() {
        this.$emit('changeItemNumber')
      }
    }
  }
  
</script>
<style>
  
</style>