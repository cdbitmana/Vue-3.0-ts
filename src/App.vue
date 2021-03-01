<template>
<div class="hidden"></div>
<div id="editor" ref="newEditorRef" class="toast-ui-editor container mx-auto"></div>
<router-link to="/list?boardId=1">제출1</router-link>
<router-link to="/list?boardId=2">제출2</router-link>
<div v-on:click="write">제출</div>
<div class="viewer-script hidden"></div>
<div id="viewer" ref="newViewRef" class="toast-ui-viewer container mx-auto"></div>
</template>

<script lang="ts">
import { defineComponent , ref , reactive , watch } from 'vue'
import Editor from '@toast-ui/editor';
import 'codemirror/lib/codemirror.css'; // Editor's Dependency Style
import '@toast-ui/editor/dist/toastui-editor.css'; // Editor's Style
import Viewer from '@toast-ui/editor/dist/toastui-editor-viewer';
import '@toast-ui/editor/dist/toastui-editor-viewer.css';
import $ from 'jquery';

export default defineComponent({
  name: 'App',
  components: {
    
  },
  props:{
    boardId: {
      type: Number,
      required: false
    }
  },
  setup(props){
   function write(){
      const editor = $('.toast-ui-editor').data('data-toast-editor');
	    const body = editor.getMarkdown().trim();
      $('.viewer-script').text(body);
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

  watch(() => props.boardId,() => {
    console.log(props.boardId);
  })

    return{
      write,
      EditorViewer__init
    }
  },
  mounted(){

function Editor__init() {
  $('.toast-ui-editor').each(function(index, node) {
	  
    var initialValue = $(node).prev().html().trim().replace(/t-script/gi, 'script');
    var editor = new Editor({
      el: node,
      previewStyle: false,
      initialValue: initialValue,
      height :500
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

  }
 
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#editor,#viewer{
  width:800px;
}

</style>