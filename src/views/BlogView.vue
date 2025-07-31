<script setup>
import MarkdownToHtml from "@/components/markdownToHtml.vue";
import { useSystem } from "@/composables/useSystem";
import { useBlogStore } from "@/stores/blogStore";
import { storeToRefs } from "pinia";
import { computed, ref } from "vue";

const { myInfo, myBlog } = storeToRefs(useBlogStore());
const { getMyBlog } = useBlogStore();

const props = defineProps({
  /**
   * id comes from the Router
   */
  id: null,
});

getMyBlog(props.id);
useSystem().changeTitle(props.id);

const myMdFile = ref("/data/markdowns/" + props.id + ".md");
const myImageFile = computed(() => "/data/images/" + myBlog.value.cover);
const myBlogDate = computed(() => {
  if (myBlog.value.date) {
    return myBlog.value.date[0] + "/" + myBlog.value.date[1] + "/" + myBlog.value.date[2];
  } else {
    return myBlog.value.date;
  }
});
</script>

<template>
  <section class="section mt-5">
    <div class="container">
      <!-- 封面图 -->
      <figure class="columns is-centered mt-5">
        <img :src="myImageFile" alt="blog cover" />
      </figure>

      <!-- 标题和信息 -->
      <div class="has-text-centered mb-4">
        <h1 class="title is-2 has-text-weight-bold">{{ myBlog.title }}</h1>
        <p class="is-size-7 has-text-grey-light">
          Posted on: {{ myBlogDate }} &nbsp;&nbsp;|&nbsp;&nbsp; Author: {{ myInfo.username }}
        </p>
      </div>

      <hr />

      <!-- Markdown内容区 -->
      <div class="columns is-centered mt-5">
        <div class="column is-10-tablet is-8-desktop is-7-widescreen markdown-content">
          <MarkdownToHtml :useNumbers="myBlog.useNumbers" :fileLocation="myMdFile" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.has-shadow {
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
  transition: box-shadow 0.3s ease;
}

.has-shadow:hover {
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.25);
}

.markdown-content {
  line-height: 1.75;
  font-size: 1rem;
  color: #4a4a4a;
}

.markdown-content img {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
}

hr {
  border-color: #dbdbdb;
}

.blog-cover {
  margin: 2rem auto 2.5rem auto;
  max-width: 600px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  overflow: hidden;
  border: 4px solid white;
  background-color: white;
}

.blog-cover img {
  display: block;
  width: 100%;
  height: auto;
  object-fit: cover;
  border-radius: 16px;
}

/* 手机端调整 */
@media screen and (max-width: 768px) {
  .blog-cover {
    max-width: 90vw;
    margin: 1.5rem auto 2rem auto;
  }
}

@media screen and (max-width: 768px) {
  .title.is-2 {
    font-size: 1.75rem;
  }
}
</style>
