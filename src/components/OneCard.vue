<template>
  <div class="card">
    <div class="card-title" @mouseup="emitSelect" ref="titleEditor">
      <editor api-key="oi6onp3p8vvf58edi8nd2jfrzjyuvzzruktd92voonnvjtsp"
                  v-model="clonedTitle"
                  :init="{
                     menubar: false,
                     toolbar: '',
                     inline: true
                  }"
      />
    </div>
    <img alt="" class="card-img" src="https://via.placeholder.com/600/92c952">
    <div class="card-body" @mouseup="emitSelect" ref="bodyEditor">
      <editor api-key="oi6onp3p8vvf58edi8nd2jfrzjyuvzzruktd92voonnvjtsp"
                  v-model="clonedBody"
                  :init="{
                     menubar: false,
                     toolbar: '',
                     inline: true
                  }"
      />
    </div>
  </div>
</template>

<script>

import Editor from '@tinymce/tinymce-vue'

export default {
  name: 'OneCard',
  components: {
    Editor
  },
  props: {
    postId: {
      type: Number,
      default: null
    },
    title: {
      type: String,
      default: ''
    },
    body: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      clonedTitle: '',
      clonedBody: ''
    }
  },
  created() {
    this.clonedTitle = this.title
    this.clonedBody = this.body
  },
  methods: {
    emitSelect(event) {
      if (this.$refs.titleEditor.contains(event.target) || this.$refs.bodyEditor.contains(event.target))
        if(window.getSelection().type === 'Range') this.$emit('text-select', window.tinymce.activeEditor.selection)
    }
  }
}
</script>

<style scoped>
.card {
  margin-bottom: 50px;
  box-shadow: 0px 17px 42px rgb(0 0 0 / 15%);
  padding: 25px;
}

.card-title {
  font-size: 24px;
  margin-bottom: 25px;
}

.card-img {
  max-width: 100%;
  margin-bottom: 25px;
  max-height: 200px;
  width: 100%;
  object-fit: cover;
}

.card-body {
  font-size: 18px;
}
</style>