<script setup>
import { useBlogStore } from "@/stores/blogStore";
import { storeToRefs } from "pinia";
import { ref } from "vue";
import { RouterLink } from "vue-router";

const { myInfo } = storeToRefs(useBlogStore());
const isBurgerOpen = ref(false);

const toggleBurgerMenu = () => {
  isBurgerOpen.value = !isBurgerOpen.value;
};

const navLinks = [
  { name: "Home", path: "/" },
  { name: "Blogs", path: "/blogs" },
  { name: "Links", path: "/links" },
  { name: "Tags", path: "/tags" },
  { name: "Tools", path: "/tools" },
  { name: "About", path: "/about" },
];
</script>

<template>
  <nav class="navbar is-fixed-top" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <RouterLink to="/" class="navbar-item is-size-4">
        {{ myInfo.blogTitle }}
      </RouterLink>

      <a
        role="button"
        class="navbar-burger"
        aria-label="menu"
        aria-expanded="false"
        @click="toggleBurgerMenu"
        :class="{ 'is-active': isBurgerOpen }">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div :class="['navbar-menu', { 'is-active': isBurgerOpen }]">
      <div class="navbar-start">
        <!-- 左侧空白区，可加LOGO或菜单 -->
      </div>

      <div class="navbar-end">
        <RouterLink
          v-for="link in navLinks"
          :key="link.path"
          :to="link.path"
          class="navbar-item"
          active-class="is-active"
          @click="isBurgerOpen = false">
          {{ link.name }}
        </RouterLink>
      </div>
    </div>
  </nav>
</template>
