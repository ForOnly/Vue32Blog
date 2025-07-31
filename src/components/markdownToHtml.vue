<script setup>
import { marked } from "marked";
import Prism from "prismjs"; // needed for the Code Block created in the markdown
import { computed, nextTick, ref } from "vue";

import "prismjs/plugins/line-numbers/prism-line-numbers.css";
import "prismjs/plugins/line-numbers/prism-line-numbers.js";

import "prismjs/plugins/toolbar/prism-toolbar.css"; // required for the following plugins
import "prismjs/plugins/toolbar/prism-toolbar.js"; // required for the following plugins

import "prismjs/plugins/copy-to-clipboard/prism-copy-to-clipboard.js"; // show copy button

import "prismjs/plugins/custom-class/prism-custom-class"; // To avoid style issues with Bulma
Prism.plugins.customClass.map({ number: "prism-number", tag: "prism-tag" });

const markDown = ref("");

const props = defineProps({
  /**
   * Location of the markdown (.md) file.
   * The location needs to be from the Public folder.
   */
  fileLocation: {
    type: String,
    default: "/data/config/blank.md",
  },
  /**
   * Show line numbering on the left side of the code when displayed in the markdown
   */
  useNumbers: {
    type: Boolean,
    default: false,
  },
});

//marked Options => https://marked.js.org/using_advanced#options
marked.setOptions({
  highlight: (code, lang) => {
    if (Prism.languages[lang]) {
      return Prism.highlight(code, Prism.languages[lang], lang);
    } else {
      return code;
    }
  },
});

const getMarkdownData = async () => {
  const response = await fetch(props.fileLocation);
  markDown.value = await response.text();
  await nextTick(); // 保证 DOM 渲染完成
  Prism.highlightAll();
};

const mdToHtml = computed(() => {
  return markDown.value ? marked.parse(markDown.value) : "Loading...";
});

getMarkdownData();
</script>

<template>
  <div class="content">
    <div :class="{ 'line-numbers': useNumbers, 'language-markup': useNumbers }" v-html="mdToHtml"></div>
  </div>
</template>

<style>
/* Apply a style to the Code Block created by marked    */
/* @import "@/assets/prism-laserwave.css"; */
@import "@/assets/prism-lucario.css";
</style>
