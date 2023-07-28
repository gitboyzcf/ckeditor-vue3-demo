<script setup>
import { reactive } from "vue";
import CKEditor from "@ckeditor/ckeditor5-vue";
import ClassicEditor from "ckeditor5-build-classic";

const state = reactive({
  editor: ClassicEditor,
  editorData: "<p>Content of the editor.</p>",
  editorConfig: {
    // The configuration of the editor.
  },
});
</script>

<template>
  <main>
    <CKEditor.component
      :editor="state.editor"
      v-model="state.editorData"
      :config="state.editorConfig"
    ></CKEditor.component>
  </main>
</template>

<style scoped lang="scss">
main {
  width: 800px;
  height: 600px;
  margin: 50px auto;
}
</style>
<style lang="scss">
.ck.ck-content{
  height: 400px;
}

</style>
