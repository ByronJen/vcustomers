<template>
  <div class="customers container">
    <Alert v-show="msg" :message="msg"></Alert>
    <div>
      <h1 class="page-header">用户管理系统</h1>
      <input class="form-control" type="text" placeholder="搜索" v-model="filterInput"/>
    </div>
    
    <br/>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(customer,index) in filterBy(customers,filterInput)" :key="index">
          <td>{{customer.username}}</td>
          <td>{{customer.phone}}</td>
          <td>{{customer.email}}</td>
          <td>
            <router-link class="btn btn-default" :to="'/detail/'+customer.id">详情</router-link>
            <router-link class="btn btn-default" :to="'/edit/'+customer.id">编辑</router-link>
            <button class="btn btn-default" @click="deleteCustomer(customer.id)">删除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'customers',
  data () {
    return {
      customers:[],
      msg:"",
      filterInput:""
    }
  },
  components:{
    Alert
  },
  methods: {
    fetchCustomers(){
      this.$http.get("http://localhost:3000/users?_sort=id&_order=desc")
      .then((response)=>{
        this.customers = response.body
      })
      .catch((error)=>{
        console.log(error)
      })
    },
    deleteCustomer(id){
      this.$http.delete("http://localhost:3000/users/"+id)
      .then((response)=>{
        this.fetchCustomers();
        this.msg = "用户删除成功！"
      })
    },
    filterBy(customres,value){
      return customres.filter(customre=>{
        return customre.username.match(value)||customre.name.match(value);
      })
    }
  },
  created() {
    if(this.$route.query.msg){
      this.msg = this.$route.query.msg;
    }
    this.fetchCustomers()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
