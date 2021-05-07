<template>
  <div>
    <div v-for="(item,index) in users" :key="index">
      <h1>{{item.name}}</h1>
      <h1>{{item.password}}</h1>
    </div>
    <button v-on:click="show">获取</button>
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
      ]
    }
  },
  methods: {
    show () {
      this.axios({
        method: 'get',
        url: '/api/users'
      }).then((response) => {
        this.users = response.data
        console.log(response)
      }).catch(function (error) {
        console.log(error)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
