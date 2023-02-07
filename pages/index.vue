<template>
  <div class="container-fluid page px-0">
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

<style>
  @font-face {
    font-family: "Caveat";
    src: local("Caveat"), url(~/assets/Caveat-VariableFont_wght.ttf) format("truetype");
  }
  @font-face {
    font-family: "Open Sans";
    src: local("Open Sans"), url(~/assets/OpenSans-VariableFont_wdth,wght.ttf) format("truetype");
  }
  .page {
    margin-bottom: 150px;
  }
  .font-primary {
    font-family: Caveat;
  }
  * {
    font-family: Open Sans
  }
</style>
