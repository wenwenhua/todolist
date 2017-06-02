<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" @keyup.enter="addNew()">
    <ul>
      <li v-for="item in items" :class="{finished : item.isFinished }" @click="toggleFinish(item)">{{item.label}}</li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
// new Vue({ //参数 })
export default {
  data: function () {
    return {
      title: 'This is a todolist',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
        // console.log(val, oldVal)
      },
      deep: true
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = ''
    }
  }
}
</script>

<style>
html{
  height: 100%;
}
body{
  display: flex;
  align-items: center;
  justify-content: center;
  height:100%;
}

.finished{
  text-decoration: line-through;
}
</style>
