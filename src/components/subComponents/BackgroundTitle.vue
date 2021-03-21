<template>
    <div class="title" :style="titleStyle">
        {{ title }}
    </div>
  
</template>

<script>
export default {
    name: 'TitleNotebook',
  props: {
      title: String,
      location: String
  },
  computed: {
    titleStyle() {
      return {
        "float": this.location
      };
    }
  }
}
</script>

<style scoped>
    .title {
      font-family: system-ui;
      font-size: 6em;
      color: #05013036;
      font-weight: 800;
    }
</style>