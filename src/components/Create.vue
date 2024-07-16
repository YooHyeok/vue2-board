<template>
  <div>
    <input v-model="writer" type="text" placeholder="글쓴이">
    <input v-model="title" type="text" placeholder="제목">
    <textarea v-model="content" placeholder="내용"/>
    <button @click="index ? update() : write()">{{ index ? "수정" : "작성"}}</button>
  </div>

</template>

<script>
import data from '@/data'
export default {
  name: 'Create',
  data () {
    const index = this.$route.params.contentId
    return {
      // data,
      writer: index ? data[index].writer : '',
      title: index ? data[index].title : '',
      content: index ? data[index].content : '',
      index
    }
  },
  methods: {
    write() {
      data.push({
        writer: this.writer,
        title: this.title,
        content: this.content,
      })
      this.$router.push({
        path: "/"
      })
    },
    update() {
        data[this.index].writer = this.writer
        data[this.index].title = this.title
        data[this.index].content = this.content

        this.$router.push({
          path: "/"
        })
        return;
    }
  }
}
</script>
