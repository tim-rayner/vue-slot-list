<script setup lang="ts">
import { ref } from "vue";
import DummyData from "@/assets/data.json";

const dummyData: any = ref();

//mock remote data fetching
setTimeout(() => {
  dummyData.value = DummyData;
}, 1250);

type Props = {
  activeIndex: Number | null;
};

const props = defineProps<Props>();
</script>

<template>
  <ul style="margin-top: 1rem" v-if="dummyData">
    <li
      v-for="(item, index) in dummyData"
      :key="item.id"
      :id="`item-${index}`"
      :class="{ active: activeIndex === index }"
    >
      <slot name="item" v-bind="item" :id="`item-${index}`" />
    </li>
  </ul>
  <div v-else>Loading...</div>
</template>

<style scoped>
ul {
  list-style-type: none;
}
ul li {
  padding: 5px 20px;
  margin: 10px;
  background: #fff;
  border: solid 1px #ddd;
}

.active {
  background: #f09865;
}
</style>
