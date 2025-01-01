<template>
  <main class="container">

    <section class="editor-section">
      <div class="editor-line-numbers">
        <div v-for="n in lineCount" :key="n" class="line-number">{{ n }}</div>
      </div>
      <textarea
        v-model="markdownText"
        class="markdown-editor"
        @input="updateLineCount"
        @scroll="syncScroll"
        ref="editor"
        spellcheck="false"
      ></textarea>
    </section>

    <section class="preview-section" v-html="renderedHTML"></section>
  </main>
</template>

<script>
import { marked } from 'marked';
import highlight from 'highlight.js';
import 'highlight.js/styles/github.css';

export default {
  name: 'MarkdownPreviewer',
  data() {
    return {
      markdownText: '',
      lineCount: 1
    };
  },
  created() {
    marked.setOptions({
      highlight: (code, lang) => {
        return highlight.highlightAuto(code).value;
      },
      breaks: true,
      gfm: true
    });

    const savedMarkdown = localStorage.getItem('markdownText');
    if (savedMarkdown) {
      this.markdownText = savedMarkdown;
      this.lineCount = savedMarkdown.split('\n').length;
    }
  },
  computed: {
    renderedHTML() {
      return marked(this.markdownText);
    }
  },
  methods: {
    updateLineCount() {
      this.lineCount = this.markdownText.split('\n').length;
      this.saveMarkdownToLocalStorage();
    },
    syncScroll(e) {
      const lineNumbers = document.querySelector('.editor-line-numbers');
      lineNumbers.scrollTop = e.target.scrollTop;
    },
    saveMarkdownToLocalStorage() {
      localStorage.setItem('markdownText', this.markdownText);
    },
    highlightSyntax() {
      const editor = this.$refs.editor;
      const selectionStart = editor.selectionStart;
      const selectionEnd = editor.selectionEnd;
      
      editor.setSelectionRange(selectionStart, selectionEnd);
    }
  },
  watch: {
    markdownText() {
      this.saveMarkdownToLocalStorage();
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  height: 100vh;

  & > * + * {
    border-left: 1px solid #d1d5db;
  }
}

.editor-section {
  position: relative;
  display: flex;
  flex: 1;
  flex-direction: column;

  .editor-line-numbers {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    width: 40px;
    overflow-y: auto;
    background: #f3f4f6;
    text-align: right;
    padding: 10px;
    box-sizing: border-box;

    &::-webkit-scrollbar {
      display: none;
    }

    .line-number {
      font-size: 14px;
      font-family: "Source Code Pro", serif;
      padding: 0 4px;
      line-height: 1.5;
    }
  }

  .markdown-editor {
    font-family: "Source Code Pro", serif;
    flex: 1;
    width: calc(100% - 40px);
    margin-left: 40px;
    border: none;
    resize: none;
    outline: none;
    padding: 10px;
    line-height: 1.57;
    color: #111827;
    caret-color: #4f46e5;
    overflow-y: auto;
    height: 100%;
    background: transparent;

    &::selection {
      color: #f9fafb;
      background: #6366f1;
    }
  }
}

.preview-section {
  font-family: ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  flex: 1;
  overflow-y: auto;
  padding: 10px;
  padding-left: 1.5rem;

  &:deep(h1),
  &:deep(h2),
  &:deep(h3),
  &:deep(h4),
  &:deep(h5),
  &:deep(h6) {
    font-weight: 600;
    line-height: 1.5;
    color: #111827;
    margin-block: 1.5rem;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid #d1d5db;
  }

  &:deep(ul),
  &:deep(ol) {
    padding-left: 2em;
    list-style-position: inside;
  }

  &:deep(ul ul),
  &:deep(ol ol),
  &:deep(ul ol),
  &:deep(ol ul) {
    margin-left: 1.5em;
  }

  &:deep(li) {
    margin-block: 0.5rem;
  }

  &:deep(img) {
    width: 100%;
    margin-block: 1.5rem;
  }

  &:deep(a) {
    color: #6366f1;
  }

  &:deep(blockquote) {
    padding-left: 1rem;
    color: #4b5563;
    border-left: 0.225em solid #d1d5db;
    margin-block: 1.5rem;
  }

  &:deep(code):not(pre code) {
    font-family: "Source Code Pro", serif;
    font-size: 0.9rem;
    background: #f3f4f6;
    margin-block: 1.5rem;
    padding: 0.2em 0.4em;
    border-radius: 3px;
  }

  &:deep(pre) {
    font-family: "Source Code Pro", serif;
    background: #f3f4f6;
    margin-block: 1.5rem;
    padding: 16px;
    overflow: auto;
    border-radius: 3px;
  }

  &:deep(table) {
    border-collapse: collapse;
    width: 100%;
    margin-block: 1.5rem;
  }

  &:deep(th) {
    background: #f3f4f6;
  }

  &:deep(th),
  &:deep(td) {
    padding: 6px 13px;
    border: 1px solid #dfe2e5;
  }

  &:deep(tr:nth-child(2n)) {
    background: #f3f4f6;
  }
}
</style>
