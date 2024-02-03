<script setup lang="ts">
import { ref, watch, type Ref } from "vue";

const emit = defineEmits(["update:modelValue"]);

const searchTerm: Ref<number | null> = ref(null);

watch(searchTerm, () => {
  emit("update:modelValue", null);
});

const findItem = () => {
  if (searchTerm.value) {
    //scroll to above the item
    const tempScroll = searchTerm.value - 1;
    const item = document.getElementById(`item-${tempScroll}`);

    if (item) {
      emit("update:modelValue", searchTerm.value ? searchTerm.value - 1 : null);
      item.scrollIntoView({ behavior: "smooth" });
    }
  }
};
</script>

<template>
  <div class="wrapper">
    <p style="padding-right: 0.5em">Scroll to list index:</p>
    <input type="number" v-model="searchTerm" />
    <button class="btn" @click="findItem">scroll</button>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
}
</style>
