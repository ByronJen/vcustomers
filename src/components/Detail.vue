<template>
  <div class="detail container">
    <h1 class="page-header">{{customer.name}}</h1>
    <ul class="list-group">
        <li class="list-group-item"><i class="glyphicon glyphicon-user"></i> {{customer.username}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-earphone"></i> {{customer.phone}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-envelope"></i> {{customer.email}}</li>
    </ul>
    <ul class="list-group">
        <li class="list-group-item"><i class="glyphicon glyphicon-record"></i> {{customer.website}}</li>
        <li class="list-group-item"><i class="glyphicon glyphicon-leaf"></i> {{customer.company.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'detail',
  data () {
    return {
        customer:{}
    }
  },
  methods:{
      fetchCustomer(id){
      this.$http.get("http://localhost:3000/users/"+id)
      .then((response)=>{
        this.customer = response.body
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
