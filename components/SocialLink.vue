<template>
  <inline-svg 
    :src="icon"
    width="50"
    height="50"
    :fill="color"
    :aria-label="ariaLabel"
    :style="customStyle"
  ></inline-svg>
</template>

<script>
import InlineSvg from 'vue-inline-svg';

export default {
  name: 'SocialLink',
  props: ["icon", "color", "ariaLabel"],
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
  margin-bottom: -2px;
  background: #f4eff3;
}
.nav-link svg {
  border: 2px solid;
  border-radius: 50%;
  padding: 13px;
}
</style>
