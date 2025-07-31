<script setup>
import { useBlogStore } from "@/stores/blogStore";
import { storeToRefs } from "pinia";

const { myInfo } = storeToRefs(useBlogStore());
</script>

<template>
  <footer class="footer custom-footer">
    <div class="content has-text-centered">
      <h3 class="footer-title">{{ myInfo.blogTitle }}</h3>
      <p class="footer-description">
        <i>{{ myInfo.description }}</i>
      </p>
      <div class="footer-divider"></div>
      <p class="footer-copyright">&copy; {{ myInfo.blogStartYear }} {{ myInfo.name }}. All rights reserved.</p>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.custom-footer {
  background-color: #f8f9fa;
  padding: 2rem 1.5rem;
  border-top: 1px solid #e0e0e0;
}

.content {
  max-width: 720px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.footer-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #333;
  margin-bottom: 0.3rem;
  line-height: 1.2;
}

.footer-description {
  font-size: 0.95rem;
  color: #666;
  margin-bottom: 1rem;
  line-height: 1.4;
}

.footer-divider {
  width: 120px;
  height: 2px;
  margin: 0 auto 1rem auto;
  background: linear-gradient(to right, transparent, #ccc, transparent);
  border-radius: 1px;
}

.footer-copyright {
  font-size: 0.85rem;
  color: #999;
  margin-top: 0.5rem;
}

@media (prefers-color-scheme: dark) {
  .custom-footer {
    background-color: #1e1e1e;
    border-top: 1px solid #333;
  }

  .footer-title {
    color: #ddd;
  }

  .footer-description {
    color: #aaa;
  }

  .footer-divider {
    background: linear-gradient(to right, transparent, #555, transparent);
  }

  .footer-copyright {
    color: #666;
  }
}
</style>
