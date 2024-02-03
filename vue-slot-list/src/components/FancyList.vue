<script setup lang="ts">
import { ref } from "vue";
import DummyData from "@/assets/data.json";

const dummyData: any = ref();

//mock remote data fetching
setTimeout(() => {
  dummyData.value = DummyData;
}, 1250);
</script>

<template>
  <ul style="margin-top: 1rem">
    <li v-if="!dummyData">Loading...</li>
    <li v-for="item in dummyData" class="item" :key="item.id">
      <slot name="item" v-bind="item" />
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style-type: none;
}
ul .item {
  padding: 5px 20px;
  margin: 10px;
  background: #fff;
  border: solid 1px #ddd;
}
</style>
