<template>
  <header :class='className'>
    <component :is='headingSize' class='text-center'>{{ content }}</component>
  </header>
</template>

<script>
const validHeadings = ['h1','h2','h3','h4','h5','h6'];

export default {
  name: 'HeadingBrush',
  props: ['content', 'marginBottom', 'headingType'],
  computed: {
    className() {
      if (!this.marginBottom) {
        return '';
      }
      return `mb-${this.marginBottom}`
    },
    headingSize() {
      if (!validHeadings.includes(this.headingType)) {
        return 'h1';
      }
      return this.headingType;
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
