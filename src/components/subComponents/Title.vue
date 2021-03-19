<template>
    <div class="title">
        {{ title }}
    </div>
  
</template>

<script>
export default {
    name: "Title",
    props: {
        title: String
    }
}
</script>

<style scoped>
    .title {
        color: white;
        font-size: 2em;
    }
</style>