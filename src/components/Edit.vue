<template>
  <div class="edit container">
    <h1 class="page-header">编辑用户</h1>
    <form @submit="editCustomer">
        <div class="well">
            <h4>用户信息</h4>
            <div class="form-group">
                <label>姓名*</label>
                <input type="text" class="form-control" placeholder="Name" v-model="customer.name">
            </div>
            <div class="form-group">
                <label>用户名</label>
                <input type="text" class="form-control" placeholder="Username" v-model="customer.username">
            </div>
            <div class="form-group">
                <label>电话*</label>
                <input type="tel" class="form-control" placeholder="Phone" v-model="customer.phone">
            </div>
            <div class="form-group">
                <label>邮箱*</label>
                <input type="email" class="form-control" placeholder="Email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label>站点</label>
                <input type="text" class="form-control" placeholder="Website" v-model="customer.website">
            </div>
            <div class="form-group">
                <label>公司</label>
                <input type="text" class="form-control" placeholder="Company" v-model="customer.company.name">
            </div>
            <button type="submit" class="btn btn-primary">确认</button>
        </div>
    </form>
  </div>
</template>
<script>
export default {
  name: 'edit',
  data () {
    return {
        customer:{
            company:{    
                name:""            
            }
        }
    }
  },
  methods:{
    fetchCustomer(id){
        this.$http.get("http://localhost:3000/users/"+id)
        .then((response)=>{
            console.log(response);
            this.customer = response.body
        })
    },
    editCustomer(id){
        if(!this.customer.name||!this.customer.phone||!this.customer.email){
            alert("星号标注为必填项，请继续完善信息");
        }else{
            this.$http.patch("http://localhost:3000/users/"+id,this.customer)
            .then((response)=>{
                this.$router.push({
                    path:"/",
                    query:{msg:"用户信息编辑成功！"}
                })
            })
        }
        e.preventDefault();
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
