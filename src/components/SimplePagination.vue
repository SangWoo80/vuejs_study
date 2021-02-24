<template>
  <div>
    <table>
      <tr>
        <th>NO</th>
        <th>TEL</th>
        <th>ADDRESS</th>
        <th>NAME</th>
      </tr>
      <tr v-for="p in paginatedData" :key="p.no">
        <td>{{ p.no }}</td>
        <td>{{ p.tel }}</td>
        <td>{{ p.address }}</td>
        <td>{{ p.name }}</td>
      </tr>
    </table>
    <div class="btn-cover">
      <button :disabled="pageNum === 0" @click="prevPage" class="page-btn">
        이전
      </button>
      <span class="page-count">{{ pageNum + 1 }} / {{ pageCount }} 페이지</span>
      <button :disabled="pageNum >= pageCount - 1" @click="nextPage" class="page-btn">
        다음
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'paginated-list',
  data () {
    return {
      pageNum: 0,
      listArray: [
        {no:'1', tel:'010-1234-0001', address:'서울', name:'홍길동1'},
        {no:'2', tel:'010-1234-0002', address:'대전', name:'홍길동2'},
        {no:'3', tel:'010-1234-0003', address:'대구', name:'홍길동3'},
        {no:'4', tel:'010-1234-0004', address:'부산', name:'홍길동4'},
        {no:'5', tel:'010-1234-0005', address:'광주', name:'홍길동5'},
        {no:'6', tel:'010-1234-0006', address:'목포', name:'홍길동6'},
        {no:'7', tel:'010-1234-0007', address:'경주', name:'홍길동7'},
        {no:'8', tel:'010-1234-0008', address:'강원도', name:'홍길동8'},
        {no:'9', tel:'010-1234-0009', address:'경기도', name:'홍길동9'},
        {no:'10', tel:'010-1234-0010', address:'경기도', name:'홍길동10'},
        {no:'11', tel:'010-1234-0011', address:'경주', name:'홍길동11'},
        {no:'12', tel:'010-1234-0012', address:'목포', name:'홍길동12'},
        {no:'13', tel:'010-1234-0013', address:'대전', name:'홍길동13'},
        {no:'14', tel:'010-1234-0014', address:'서울', name:'홍길동14'},
        {no:'15', tel:'010-1234-0015', address:'서울', name:'홍길동15'},
        {no:'16', tel:'010-1234-0016', address:'광주', name:'홍길동16'},
        {no:'17', tel:'010-1234-0017', address:'광주', name:'홍길동17'},
        {no:'18', tel:'010-1234-0018', address:'청주', name:'홍길동18'},
        {no:'19', tel:'010-1234-0019', address:'청주', name:'홍길동19'}
      ]
    }
  },
  props: {
    // listArray: {
    //   상위 페이지에서 axios 로 호출하여 데이터를 넘기는데 테스트 하기 위해 주석 처리후 data 임의 생성 
    //   참고 URL : https://pewww.tistory.com/5
    //   type: Array,
    //   required: true
    // },
    pageSize: {
      type: Number,
      required: false,
      default: 10
    }
  },
  methods: {
    nextPage () {
      this.pageNum += 1;
    },
    prevPage () {
      this.pageNum -= 1;
    }
  },
  computed: {
    pageCount () {
      let listLeng = this.listArray.length,
          listSize = this.pageSize,
          page = Math.floor(listLeng / listSize);
      if (listLeng % listSize > 0) page += 1;
      
      /*
      아니면 page = Math.floor((listLeng - 1) / listSize) + 1;
      이런식으로 if 문 없이 고칠 수도 있다!
      */
      return page;
    },
    paginatedData () {
      const start = this.pageNum * this.pageSize,
            end = start + this.pageSize;
      return this.listArray.slice(start, end);
    }
  }
}
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
}
table th {
  font-size: 1.2rem;
}
table tr {
  height: 2rem;
  text-align: center;
  border-bottom: 1px solid #505050;
}
table tr:first-of-type {
  border-top: 2px solid #404040;
}
table tr td {
  padding: 1rem 0;
  font-size: 1.1rem;
}
.btn-cover {
  margin-top: 1.5rem;
  text-align: center;
}
.btn-cover .page-btn {
  width: 5rem;
  height: 2rem;
  letter-spacing: 0.5px;
}
.btn-cover .page-count {
  padding: 0 1rem;
}
</style>