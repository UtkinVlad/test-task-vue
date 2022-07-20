<template>
  <div class="main">
    <div class="card-group">
      <OneCard v-for="post in postList" :key="post.id" :title="post.title" :body="post.body"/>
      <button v-if="!noMorePosts" class="card-btn" @click="addOnePostToList">Добавить еще</button>
    </div>
  </div>
</template>

<script>

import OneCard from '@/components/OneCard'

export default {
  name: 'PostCards',
  components: {OneCard},
  data() {
    return {
      postList: [],
      noMorePosts: false,
      postCount: 0
    }
  },
  created() {
    this.loopAddPost(3)
  },
  methods: {
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
.card-btn:hover {
  background: #bbb;
  color: #fff;
}
</style>