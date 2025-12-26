

<script setup>
import { computed } from 'vue'
import { marked } from 'marked'
import hljs from 'highlight.js'

import 'github-markdown-css/github-markdown.css'
import 'highlight.js/styles/github.css'

import md from "./htaq.md?raw"

marked.setOptions({
  highlight(code, lang) {
    if (lang && hljs.getLanguage(lang)) {
      return hljs.highlight(code, { language: lang }).value
    }
    return hljs.highlightAuto(code).value
  }
})

const html = computed(() => marked.parse(md))
</script>

<template>
  <div class="markdown" v-html="html"></div>
</template>

<style>
.markdown {
  max-width: 800px;
  margin: 40px auto;
  padding: 24px;
  background: white;
  border-radius: 8px;
}
body {
  background: #f5f5f5;
}
</style>
