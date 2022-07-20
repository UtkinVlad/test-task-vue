<template>
  <div class="card">
    <div class="card-title">
      <editor id="test"
            api-key="oi6onp3p8vvf58edi8nd2jfrzjyuvzzruktd92voonnvjtsp"
            v-model="clonedTitle"
            :init="{
             menubar: false,
             toolbar: '',
             inline: true
            }"
      />
    </div>
    <img alt="" class="card-img" src="https://via.placeholder.com/600/92c952">
    <div class="card-body">
      <editor
          api-key="oi6onp3p8vvf58edi8nd2jfrzjyuvzzruktd92voonnvjtsp"
          v-model="clonedBody"
          :init="{
           menubar: false,
           toolbar: '',
           inline: true
         }"/>
    </div>
    <button class="card-btn" @click="switchItalic">Курсив</button>
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
    switchItalic() {
      window.tinymce.execCommand('italic')
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

.card-btn {
  background: #fff;
  color: #bbb;
  border: 1px solid #bbbbbb;
  border-radius: 4px;
  padding: 5px 10px;
  cursor: pointer;
}

.card-btn:hover {
  background: #bbb;
  color: #fff;
}
</style>