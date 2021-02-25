<template>
<div class="hidden"></div>
<div id="editor" ref="newEditorRef" class="toast-ui-editor container mx-auto"></div>
<div v-on:click="write">제출</div>
<div class="viewer hidden"></div>
<div id="viewer" ref="newViewRef" class="toast-ui-viewer container mx-auto"></div>
</template>

<script lang="ts">
import { defineComponent , ref , reactive } from 'vue'
import Editor from '@toast-ui/editor';
import 'codemirror/lib/codemirror.css'; // Editor's Dependency Style
import '@toast-ui/editor/dist/toastui-editor.css'; // Editor's Style
import Viewer from '@toast-ui/editor/dist/toastui-editor-viewer';
import '@toast-ui/editor/dist/toastui-editor-viewer.css';

export default defineComponent({
  name: 'App',
  components: {
    
  },
  setup(){
   function write(){
  const editor = $('.toast-ui-editor').data('data-toast-editor');
	const body = editor.getMarkdown().trim();
  $('.viewer').text(body);
  EditorViewer__init();
    }

    function EditorViewer__init() {
  $('.toast-ui-viewer').each(function(index, node) {
    var initialValue = $(node).prev().html().trim().replace(/t-script/gi, 'script');
    var viewer = new Viewer({
      el: node,
      initialValue: initialValue
          });
  });
}

    return{
      write,
      EditorViewer__init
    }
  },
  mounted(){
  const newEditorRef = ref();
  const newViewRef = ref();

function Editor__init() {
  $('.toast-ui-editor').each(function(index, node) {
	  
    var initialValue = $(node).html().trim().replace(/t-script/gi, 'script');
    var editor = new Editor({
      el: node,
      previewStyle: false,
      initialValue: initialValue,
      height:500
    });
    $(node).data('data-toast-editor', editor);
  });
}

Editor__init();


function EditorViewer__init() {
  $('.toast-ui-viewer').each(function(index, node) {
    var initialValue = $(node).prev().html().trim().replace(/t-script/gi, 'script');
    var viewer = new Viewer({
      el: node,
      initialValue: initialValue
          });
  });
}
EditorViewer__init();

return{
  newEditorRef,
  newViewRef
}


  }
 
})


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#editor,#viewer{
  width:800px;
}

</style>