<script setup lang="ts">
import FancyList from "@/components/FancyList.vue";
</script>

<template>
  <div class="">
    <FancyList>
      <template #item="{ body, username, likes }">
        <div class="item">
          <p>{{ body }}</p>
          <p class="meta">by {{ username }} | {{ likes }} likes</p>
        </div>
      </template>
    </FancyList>
  </div>
</template>
