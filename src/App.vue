<script setup>
import TheFooterBar from "@/components/theFooterBar.vue";
import TheNavBar from "@/components/theNavBar.vue";
import { useBlogStore } from "@/stores/blogStore";
import { RouterView } from "vue-router";

const { getMyBlogs } = useBlogStore();

getMyBlogs();
</script>
<template>
  <div class="layout-wrapper">
    <TheNavBar />

    <section class="section main-content">
      <div class="container">
        <RouterView />
      </div>
    </section>

    <TheFooterBar />
  </div>
</template>

<style>
#app {
  /* font-family: "Roboto", Helvetica, Arial, sans-serif;
  text-align: center; */
  width: 100%;
  height: 100%;
}
.layout-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.main-content {
  flex: 1;
}
</style>
