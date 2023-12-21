
<template>
  <div class="flex flex-wrap w-full  bg-slate-800">
    <h1 class="w-full text-center text-3xl  text-yellow-400 my-4">Markdown App</h1>
    <section class="flex m-auto w-10/12 h-screen">
      <article class="w-1/2 border">
        <textarea
          ref="markdownTextArea"
          class="w-full h-full"
          :value="text"
          @input="update"
        ></textarea>
      </article>
      <article class="bg-slate-400 w-60  text-center p-5 " v-html="markedText"></article>
    </section>
  </div>
</template>

<script>
import { marked } from 'marked';
import useDebounce from './usedebounce.js'
export default {
  data() {
    return {
      text: "**this is markdown app**",
      debounce: "",
    };
  },
  computed: {
    markedText() {
      return marked(this.text);
    },
  },
  methods: {
    update(e) {
      const task = () => (this.text = e.target.value);
      this.debounce(task, 500);
    },
  },
  mounted() {
    this.debounce = useDebounce();
    this.$refs.markdownTextArea.focus();
  },
};
</script>

<style></style>