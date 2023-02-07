<template>
  <header :class='className'>
    <h2 class='text-center'>{{ content }}</h2>
  </header>
</template>

<script>
export default {
  name: 'HeadingBrush',
  props: ['content', 'marginBottom'],
  computed: {
    className() {
      if (!this.marginBottom) {
        return '';
      }
      return `mb-${this.marginBottom}`
    }
  }
}
</script>

<style scoped>
  header {
    position: relative;
  }
  header h2 {
    position: relative;
    z-index: 2;
   }
  header::before {
    content: "";
    position: absolute;
    z-index: 1;
    top: 50%;
    left: 0;
    width: 100%;
    height: 100%;
    background: url(/brush.webp);
    background-repeat: no-repeat;
    background-position: center bottom;
    background-size: contain;
    opacity: 0.3;
  }
</style>
