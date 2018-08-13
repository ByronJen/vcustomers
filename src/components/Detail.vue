<template>
  <div class="detail container">
    <h1 class="page-header">
      {{customer.name}}
      <div class="pull-right">
        <router-link tag="span" class="btn btn-primary" :to="'/edit/'+customer.id">编辑</router-link>
        <span class="btn btn-default" @click="deleteCustomer(customer.id)">删除</span>
      </div>
    </h1>
    <ul class="list-group">
        <li class="list-group-item"><i class="glyphicon glyphicon-user"></i> {{customer.username}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-earphone"></i> {{customer.phone}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-envelope"></i> {{customer.email}}</li>
    </ul>
    <ul class="list-group">
        <li class="list-group-item"><i class="glyphicon glyphicon-record"></i> {{customer.website}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-leaf"></i> {{customer.company.name}}</li>
    </ul>
    <router-link to="/" class="btn btn-default">返回</router-link>
  </div>
</template>

<script>
export default {
  name: 'detail',
  data () {
    return {
      customer:{
        company:{            
        }
      }
    }
  },
  methods:{
    fetchCustomer(id){
      this.$http.get("http://localhost:3000/users/"+id)
      .then((response)=>{
        this.customer = response.body
      })
    },
    deleteCustomer(id){
      this.$http.delete("http://localhost:3000/users/"+id)
      .then((response)=>{
        this.$router.push({
            path:"/",
            query:{msg:"用户删除成功！"}
        })
      })
    }
  },
  created(){
      this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
