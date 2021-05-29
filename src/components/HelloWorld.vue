<template>
  <div>
    <div>Selamat Datang</div>
    <ul>
    <li v-for="item in todos" :key="item.Id">{{ item.desk }} <button @click="hapus(item.Id)">X</button></li>
    </ul>
    <input v-model="myText"/>
    <button @click="tambah">Add</button>
  </div>
  
</template>

<script>
import axios from 'axios'
export default {
  data: function () {
    return {
      todos: [],
      myText: ''
    }
  },
  created: function() {
    axios.get('http://localhost:3000/todo')
    .then(result => {
      this.todos = result.data
    })
  },
  methods: {
    tambah: function () {
      const newItem = { desk : this.myText }
      axios.post('http://localhost:3000/todo', newItem)
      this.todos.push(newItem)
    },
    hapus: function (id) {
      axios.delete(`http://localhost:3000/todo/${id}`)
    }
  }
}
</script>
