<script setup lang="ts">
import FancyList from "@/components/FancyList.vue";
import { ref, watch, type Ref } from "vue";
import DummyData from "@/assets/data.json";

const dummyData: any = ref();

const searchTerm: Ref<number | null> = ref(null);
const activeIndex: Ref<number | null> = ref(null);

setTimeout(() => {
  dummyData.value = DummyData;
}, 1250);

watch(searchTerm, () => {
  activeIndex.value = null;
});

const findItem = () => {
  if (searchTerm.value) {
    //scroll to the item
    //scroll to above the item
    const tempScroll = searchTerm.value - 1;
    const item = document.getElementById(`item-${tempScroll}`);

    if (item) {
      activeIndex.value = searchTerm.value ? searchTerm.value - 1 : null;
      item.scrollIntoView({ behavior: "smooth" });
    }
  }
};
</script>

<template>
  <div class="">
    <input type="number" v-model="searchTerm" />
    <button class="btn" @click="findItem">Find</button>

    <FancyList class="item" :activeIndex="activeIndex">
      <template #item="{ body, username, likes }">
        <!-- content here-->
        <div class="item">
          <p>{{ body }}</p>
          <p class="meta">by {{ username }} | {{ likes }} likes</p>
        </div>
      </template>
    </FancyList>
  </div>
</template>
