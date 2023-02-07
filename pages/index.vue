<template>
  <div class="container-fluid px-0">
    <Banner />
    <Articles />
    <Newsletter />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>

<style scoped>
  .container-fluid {
    margin-bottom: 150px;
  }
</style>
