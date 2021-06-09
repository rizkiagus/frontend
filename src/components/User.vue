<template>
  <div>
    <h1>List User</h1>
    <ul>
    <li v-for="item in todos" :key="item.Id">{{ item.desk }} <button @click="hapus(item.Id)">X</button></li>
    </ul>
    <input v-model="username"/>
    <input v-model="password"/>
    <button @click="tambah">Add</button>
  </div>
  
</template>

<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      users: [],
      username: '',
      password: ''
    }
  },
  created: function() {
    const username = localStorage.getItem('usr')
    const password = localStorage.getItem('pwd')
    axios.get('http://localhost:3000/user', { headers: {username, password}})
    .then(result => {
      this.users = result.data
    })
  },
  methods: {
    tambah: function () {
      const user = localStorage.getItem('usr')
      const pass = localStorage.getItem('pwd')
      const newItem = { username : this.username, password : this.password }
      axios.post('http://localhost:3000/user', newItem, { headers: {username: user, password: pass}})
      this.users.push(newItem)
    },
    hapus: function (id) {
      const username = localStorage.getItem('usr')
      const password = localStorage.getItem('pwd')
      axios.delete(`http://localhost:3000/todo/${id}`, { headers: {username, password}})
    }
  }
}
</script>
