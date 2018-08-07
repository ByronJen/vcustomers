<template>
  <div class="add container">
    <h1 class="page-header">添加用户</h1>
    <form @submit="addCustomer">
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
            <button type="submit" class="btn btn-primary">提交</button>
        </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
        customer:{
            company:{
                
            }
        }
    }
  },
  methods:{
      addCustomer(e){
        if(!this.customer.name||!this.customer.phone||!this.customer.email){
            alert("星号标注为必填项，请继续完善信息");
        }else{
            this.$http.post("http://localhost:3000/users",this.customer)
            .then((response)=>{
                this.$router.push({
                    path:"/",
                    query:{msg:"用户信息添加成功！"}
                })
            })
        }
        e.preventDefault();
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
