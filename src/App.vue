<template>
  <div class="wrapper">
    <section class="two-column-picker">
      <item-list :items="leftData" :max-picked="6" />
      <item-list :items="rightData" />
    </section>
  </div>
</template>

<script setup lang="ts">
import ItemList from "./components/itemList.vue";
import leftData from "@/data/left.json";
import rightData from "@/data/right.json";
</script>

<style scoped lang="scss">
.wrapper {
  width: 100%;
  height: 100dvh;
  display: flex;
  align-items: center;
  justify-content: center;
  .two-column-picker {
    position: relative;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    max-width: 600px;
  }
}
</style>
