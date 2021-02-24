<template>
  <div class="about">
    <ul class="list-group">
      <li v-for="item in studyList" v-bind:key="item.id" class="list-group-item">
        {{item.id}}. {{item.title}} ☞
        <button v-on:click="pageLink(item.id)">이동</button>
      </li>      
    </ul>
  </div>
</template>

<script>
export default {
  name: 'about',
  data() {
    return {
      studyList: [
        {
          id: 1, title: 'simple 페이징 처리'
        }
      ]
    }
  },
  methods: {
    pageLink(id) {
      // object
      // this.$router.push({ path: '/simplePagination' })
      // // 이름을 가지는 라우트
      // router.push({ name: 'user', params: { userId: 123 }})
      // // 쿼리와 함께 사용, 결과는 /register?plan=private
      // router.push({ path: 'register', query: { plan: 'private' }})

      console.log(">>>>> pageLink (" + id + ") <<<<<");

      if( id == 1 ) {
        console.log("> simplePagination");
        this.$router.push({ path: '/simplePagination' });
      }
    }
  }
}
</script>

<style scoped>

</style>
