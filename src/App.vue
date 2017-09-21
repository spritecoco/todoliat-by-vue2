<template>
  <div id="app">
      <h1 v-text="title"></h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item , isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p>child tell me :{{childWords}}</p>
    <component-a msgfromfather = 'hello' v-on:child-say="listenToMyBoy"></component-a>
  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/componebtA.vue'
export default {
  data: function () {
    return {
      title: 'this is a example',
      items: Store.fetch(),
      newItems: '',
      childWords: ''
    }
  },
  components: { ComponentA },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
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
        isFinished: true
      })
    },
    listenToMyBoy: function (msg) {
      this.childWords = msg
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished {
  text-decoration: underline;
}
</style>
