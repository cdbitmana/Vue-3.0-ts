<template>
  <div>gkgk</div>
</template>

<script lang="ts">
import { defineComponent , ref , reactive , watch } from 'vue'

export default defineComponent ({
  name: 'test',
  components: {

  },
  props: {
    boardId: Number
  },
  setup(props){
    watch(() => props.boardId,() => {
    console.log(props.boardId);
  })
  }


})
</script>

<style>

</style>