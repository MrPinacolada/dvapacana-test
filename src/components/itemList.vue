<template>
  <section class="picker">
    <div class="picker__display">
      <span class="picker__display--items">
        <button
          class="item"
          v-for="(item, index) in pickedItems"
          :key="item.id"
          @click="removeItem(index)"
        >
          {{ item.name }}
        </button>
      </span>
      <p class="picker__display--counter">
        Picked items {{ pickedItems.length }} / {{ maxPicked }}
      </p>
    </div>
    <div class="picker__list">
      <button
        class="picker__list--item"
        v-for="item in availableItems"
        :key="item.id"
        @click="pickItem(item)"
      >
        {{ item.name }}
      </button>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";

interface IProps {
  items: { id: number; name: string }[];
  maxPicked?: number;
}

type Item = (typeof props.items)[number];

const props = defineProps<IProps>();

const maxPicked = props.maxPicked ?? 1;
const pickedItems = ref<Item[]>([]);

const availableItems = computed(() =>
  props.items.filter((item) => !pickedItems.value.includes(item))
);

const pickItem = (item: Item) => {
  if (pickedItems.value.length < maxPicked) {
    pickedItems.value.push(item);
  }
};

const removeItem = (index: number) => {
  pickedItems.value.splice(index, 1);
};
</script>
<style scoped lang="scss">
.picker {
  display: grid;
  align-items: center;
  justify-items: center;
  gap: 20px;
  &__list {
    position: relative;
    width: 100%;
    height: 100%;
    border: 1px gray solid;
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    justify-content: flex-start;
    gap: 20px;
    padding: 10px;
    border-radius: 5px;
    &--item {
      border: none;
      outline: none;
      cursor: pointer;
      padding: 5px 12px;
      margin: 0;
      background-color: rgb(187, 159, 159);
      border-radius: 12px;
      transition: background-color 0.3s ease;
      will-change: background-color;
      &:hover {
        background-color: antiquewhite;
      }
      &:active {
        background-color: rgb(198, 164, 122);
      }
    }
  }
  &__display {
    position: relative;
    width: 100%;
    height: 100%;
    border: 1px gray solid;
    display: grid;
    gap: 10px;
    padding: 10px;
    border-radius: 5px;
    align-content: space-between;
    &--items {
      display: flex;
      align-items: center;
      justify-content: flex-start;
      flex-wrap: wrap;
      gap: 8px;
      .item {
        background-color: aquamarine;
        border-radius: 12px;
        padding: 8px 12px;
      }
    }
  }
}
</style>
