<script setup>
import { reactive } from "vue";
import CKEditor from "@ckeditor/ckeditor5-vue";
import ClassicEditor from "ckeditor5-build-classic";
import plainTextToHtml from '@ckeditor/ckeditor5-clipboard/src/utils/plaintexttohtml'

const state = reactive({
  editor: ClassicEditor,
  editorData: "<p>Content of the editor.</p>",
  editorConfig: {
    // The configuration of the editor.
  },
});

const onReady = (editor) => {
  editor.plugins
    .get("ClipboardPipeline")
    .on("inputTransformation", (evt, data) => {
      const dataTransfer = data.dataTransfer;
      console.log(dataTransfer);
      let content = plainTextToHtml(dataTransfer.getData("text/plain"));
      console.log(content);
      data.content = editor.data.htmlProcessor.toView(content);
    });
};
</script>

<template>
  <main>
    <CKEditor.component
      :editor="state.editor"
      v-model="state.editorData"
      :config="state.editorConfig"
      @ready="onReady"
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
.ck.ck-content {
  height: 400px;
}
</style>
