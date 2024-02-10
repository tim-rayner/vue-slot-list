<script setup lang="ts">
import FancyList from "@/components/FancyList.vue";
import SearchInput from "@/components/SearchInput.vue";
import { ref, type Ref } from "vue";

const activeIndex: Ref<number | null> = ref(null);

const openInNewTab = (url: string) => {
  const newWindow = window.open(url, "_blank", "noopener,noreferrer");
  if (newWindow) newWindow.opener = null;
};
</script>

<template>
  <div class="app">
    <h1>Ticketmaster Rap Events (top 50)</h1>
    <SearchInput v-model="activeIndex" />
    <FancyList class="item" :activeIndex="activeIndex">
      <template #item="{ name, date, venue, country, city, url }">
        <!-- content here-->
        <div class="item" @click="openInNewTab(url)">
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
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 2rem;
  margin: auto;
}

h1 {
  text-align: center;
  margin-top: 2rem;
}

.meta {
  font-size: 0.8rem;
  color: #666;
}
</style>
