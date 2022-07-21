<template>
  <div class="main">
    <div class="card-action">
      <button class="card-btn"
                  :class="italicButtonActive ? 'active' : '' "
                  @click="switchItalic"
                  v-click-outside="clickOutsideItalicButton">
        Курсив
      </button>
      <button v-if="!noMorePosts" class="card-btn" @click="addOnePostToList">Добавить еще</button>
    </div>
    <div class="card-group">
      <OneCard v-for="post in postList"
                :key="post.id"
                :title="post.title"
                :body="post.body"
                @text-select="inspectSelection"
      />
    </div>
  </div>
</template>

<script>

import OneCard from '@/components/OneCard'
import vClickOutside from 'v-click-outside'

export default {
  name: 'PostCards',
  components: {OneCard},
  directives: {
    clickOutside: vClickOutside.directive
  },
  data() {
    return {
      postList: [],
      noMorePosts: false,
      postCount: 0,
      italicButtonActive: false,
      italicSelected: false
    }
  },
  created() {
    this.loopAddPost(3)
  },
  methods: {
    inspectSelection(selection) {
      if (selection.getNode().nodeName === 'EM') {
        this.italicButtonActive = true
        this.italicSelected = true
      }
    },
    clickOutsideItalicButton() {
      if (!this.italicSelected) this.italicButtonActive = false
      this.italicSelected = false
    },
    switchItalic() {
      window.tinymce.activeEditor.execCommand('italic')
      this.italicButtonActive = !this.italicButtonActive
    },
    loopAddPost(count) {
      for (let counter = 0; counter < count; counter++) this.addOnePostToList()
    },
    async addOnePostToList() {
      this.postCount++
      if (this.isLimitReached()) return

      const response = await this.axios.get('https://jsonplaceholder.typicode.com/posts/' + this.postCount)
      this.postList.push(response.data)
    },
    isLimitReached() {
      if (this.postCount > 100) {
        this.noMorePosts = true
        return true
      }
      return false
    }
  }
}
</script>

<style scoped>
.card-action {
  width: 300px;
  position: fixed;
  left: 100px;
  top: 100px;
}
.main {
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;;
  margin: 50px 0;
}
.card-group {
  display: flex;
  flex-flow: column wrap;
  width: 500px;
}
.card-btn {
  background: #fff;
  color: #bbb;
  border: 1px solid #bbbbbb;
  border-radius: 4px;
  padding: 5px 10px;
  cursor: pointer;
}
.active {
  background: #bbb;
  color: #fff;
}
.card-btn:hover {
  background: #bbb;
  color: #fff;
}
</style>