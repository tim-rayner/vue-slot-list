<script setup lang="ts">
import FancyList from "@/components/FancyList.vue";
import SearchInput from "@/components/SearchInput.vue";
import { ref, type Ref } from "vue";

const activeIndex: Ref<number | null> = ref(null);
</script>

<template>
  <div class="">
    <h1>Ticketmaster Rap Events</h1>
    <SearchInput v-model="activeIndex" />
    <FancyList class="item" :activeIndex="activeIndex">
      <template #item="{ name, date, venue, country, city }">
        <!-- content here-->
        <div class="item">
          <p>{{ name }}</p>
          <p class="meta">
            {{ date }} | {{ venue }} | {{ country }} - {{ city }}
          </p>
        </div>
      </template>
    </FancyList>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  margin-top: 2rem;
}

.meta {
  font-size: 0.8rem;
  color: #666;
}
</style>
