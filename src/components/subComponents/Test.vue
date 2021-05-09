<template>
    <div class="item">
        <p> {{ item }} test </p>
    </div>
</template>

<script>
export default {
    name: "Item",
    props: {
        item: Array
    },
    setup() {
        console.log("TEST");
    },
}
</script>

<style>

  .item {
    background-color: #b6a4d636;
    border-radius: 4px;
    padding: 1em 2em;
    margin-bottom: 1em;
  }
</style>