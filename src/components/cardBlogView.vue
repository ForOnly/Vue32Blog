<script setup>
import { computed } from "vue";
import { RouterLink } from "vue-router";

const props = defineProps({
  /**
   * The value to group the cards together
   */
  blog: {},
  /**
   * The cover to use on the card.
   * This allows the images to be loaded faster as the page is created
   */
  cover: null,
});

const imageFile = computed(() => "/data/images/" + props.blog.cover);
</script>

<template>
  <div class="column is-one-third">
    <RouterLink :to="`/blog/${blog.id}`" class="blog-card-link">
      <div class="card blog-card is-small">
        <div class="card-image">
          <figure class="image is-4by3 blog-card-image">
            <img :src="imageFile" alt="Cover image" />
          </figure>
        </div>
        <div class="card-content">
          <div class="content">
            <h3 class="title is-6 mb-2">{{ blog.title }}</h3>
            <p class="is-size-7 has-text-grey mb-2">{{ blog.date[0] }}/{{ blog.date[1] }}/{{ blog.date[2] }}</p>
            <p class="is-size-7 has-text-grey-dark mb-3">
              {{ blog.des }}
            </p>
            <div class="tags are-small">
              <span v-for="(tag, i) in blog.tags" :key="i" class="tag is-light is-rounded">
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </RouterLink>
  </div>
</template>

<style lang="scss" scoped>
.blog-card-link {
  text-decoration: none;
  color: inherit;
  display: block;
}

.blog-card {
  max-width: 320px;
  height: 400px; // 卡片高度统一
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  border-radius: 12px;
  overflow: hidden;
  transition:
    box-shadow 0.3s ease,
    transform 0.3s ease;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
  background-color: white;

  &:hover {
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
    transform: translateY(-3px);
  }
}

.blog-card-image {
  flex-shrink: 0;
}

.blog-card-image img {
  width: 100%;
  height: 160px; // 固定图片高度
  object-fit: cover;
  border-radius: 12px 12px 0 0;
}

.card-content {
  padding: 0.75rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card-content .content {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.title {
  font-size: 1rem;
  margin-bottom: 0.5rem;
  flex-shrink: 0;
}

.description-text {
  flex-grow: 1;
  font-size: 0.8rem;
  color: #555;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3; /* 限制显示3行 */
  -webkit-box-orient: vertical;
}

.tags {
  margin-top: auto;
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.tag {
  font-size: 0.7rem;
  padding: 0.3em 0.8em;
  border-radius: 999px;
  background-color: #f0f0f0;
  color: #555;
  transition: all 0.3s ease;
  cursor: default;

  &:hover {
    background-color: #e0e0e0;
    color: #333;
  }
}
</style>
