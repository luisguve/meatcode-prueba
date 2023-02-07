<template>
  <a class="nav-link" :href="url">
    <inline-svg 
      :src="icon"
      width="50" 
      height="50"
      :fill="color"
      aria-label="My image"
      :style="customStyle"
  ></inline-svg>
  </a>
</template>

<script>
import InlineSvg from 'vue-inline-svg';

export default {
  name: 'SocialLink',
  props: ["icon", "color", "url"],
  components: {
    InlineSvg
  },
  computed: {
    customStyle: function() {
      return `border-color: ${this.color}`
    }
  }
}
</script>

<style scoped>
svg {
  display: inline-block;
  vertical-align: baseline;
  margin-bottom: -2px; /* yes, I'm that particular about formatting */
}
.nav-link svg {
  border: 2px solid;
  border-radius: 50%;
  padding: 13px;
}
</style>
