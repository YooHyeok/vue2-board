<template>
  <div>
    <table>
      <tr>
        <th>글쓴이</th>
        <th>제목</th>
        <th>내용</th>
      </tr>
      <tr 
      :key="index"
      v-for="(value, index) in data" @click="detail(index)">
        <td>{{value.writer}}</td>
        <td>{{value.title}}</td>
        <td>{{value.content}}</td>
      </tr>
    </table>
    <button @click="write"> 글쓰기 </button>
  </div>
</template>

<script>
import data from '@/data'
export default {
  name: 'Read',
  data () {
    return {
      data
    }
  },
  methods: {
    write() {
      this.$router.push({
        path: 'create'
      })
    },
    detail(index) {
      this.$router.push({
        name: 'Detail',
        params: {
          contentId: index
        }
      })
    }
  }
}
</script>
