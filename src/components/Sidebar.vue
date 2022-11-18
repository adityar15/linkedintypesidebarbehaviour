<template>
  <div class="flex flex-col space-y-4">
    <SidebarCard class="h-72" />
    <SidebarCard class="h-28" ref="secondLastCard" />
    <SidebarCard class="h-96" :class="{ 'fixed top-20': !isVisible }" />
  </div>
</template>

<script setup lang="ts">
import { defineAsyncComponent, onMounted, ref } from "vue";

const SidebarCard = defineAsyncComponent(() => import("./SidebarCard.vue"));

const secondLastCard = ref<typeof SidebarCard>();

const isVisible = ref<boolean>(true);

onMounted(() => {
  window.addEventListener("scroll", () => 
  trackVisibility()
  );
});

function trackVisibility(): void {
  const rect = secondLastCard.value?.$el.getBoundingClientRect();
  isVisible.value =
    rect?.top >= 0 &&
    rect?.left >= 0 &&
    rect?.bottom <=
      (window.innerHeight || document.documentElement.clientHeight) &&
    rect?.right <= (window.innerWidth || document.documentElement.clientWidth);
}
</script>

<style scoped></style>
