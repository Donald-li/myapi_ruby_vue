<template>
  <div>
    <div v-for="(item,index) in users" :key="index">
      <div>账号ID：{{item.id}} 账号：{{item.name}} 密码：{{item.password}}</div>
    </div>
    <button v-on:click="show">获取</button>
    <br>
    <form id="userForm">
      <label>用户名</label>
      <input type="text" id="username" v-model="username">
      <br>
      <label>密码</label>
      <input type="password" id="userpassword" v-model="userpassword">
      <br>
      <button v-on:click="save">注册</button>
    </form>
    <form>
      <label>用户名</label>
      <input type="text" v-model="username_log">
      <br>
      <label>密码</label>
      <input type="password" v-model="userpassword_log">
      <br>
      <button v-on:click="verification()">登陆</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      users: [
        {
          'id':1,
          'name': 'donald1',
          'password': '1234'
        },
        {
          'id': 2,
          'name': 'donald2',
          'password': '1234'
        }
      ],
      username:'默认名',
      userpassword:'123',
      username_log:'默认名',
      userpassword_log:'123'
    }
  },
  methods: {
    show () {
      this.axios({
        method: 'get',
        url: '/api/users'
      }).then((response) => {
        this.users = response.data
      }).catch(function (error) {
        console.log(error)
      })
    },
    save(){
      this.axios({
        method: 'post',
        url: '/api/users',
        data: {
          name: this.username,
          password: this.userpassword
        },
      }).then((response)=>{
        // this.show()
      })
    },
    //用户登录验证
    verification(){
      this.axios({
        method:"post",
        url: '/api/users/verification',
        data:{
          id: this.username_log,
          password: this.userpassword_log
        }
      }).then((response)=>{
          if(response.data.state==null) {
            alert(response.data.name)
          }else{
            alert(response.data.msg)
          }
      })
    }
  },
  mounted () {
    this.show()
    //轮询
    window.setInterval(this.show,5000)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
