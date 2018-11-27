<template>
  <div class="container mt-5">
    <p>狀態 : {{status}}</p>
    <div class="form-inline mb-3">
      <input type="text" class="form-control" v-model="userName">
      <div class="btn btn-primary" @click="updateUserName">更新</div>
    </div>
    <table class="table table-striped table-dark">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Image</th>
          <th scope="col">First</th>
          <th scope="col">Last</th>
          <th scope="col">Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,id) in listData" :key="id" :class='{ "bg-info" : item.selected }'>
          <td scope="row">{{id+1}}</td>
          <td>
            <img :src="item.picture.medium" width="50px">
          </td>
          <td>{{item.name.first}}</td>
          <td>{{item.name.last}}</td>
          <td>{{item.email}}</td>
          <td>
            <button class="btn btn-outline-primary" @click='clickMe(item)'>點我</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {

  data() {
    return {
      msg: "Welcome",
      listData: [],
      userName: "xdf",
      status: this.$store.state.status
    };
  },
  methods: {
    getData() {
      this.axios
        .get("https://randomuser.me/api/1.2/?results=10")
        .then(response =>{
          // 成功回應
          this.listData = response.data.results;
          this.listData.forEach(item => {
            this.$set(item , 'selected', false)
          })
        })
        .catch(error => {
          // 失敗回應
          alert(error);
        });
    },
    updateUserName() {
      this.$emit('pushNewname',this.userName)
    },
    clickMe(item){
      item.selected = !item.selected

    }
  },
  mounted() {
    this.getData();
  }
};
</script>

<style>
</style>
