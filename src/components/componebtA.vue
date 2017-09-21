<template>
  <div id="app">
     <h1>{{msg}}</h1>
    <h2>{{msgfromfather}}</h2>
    <button v-on:click="onClickMe">Click Me!!!</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      msg: 'hello from component-a'
    }
  },
  props: ['msgfromfather'],
  methods: {
    onClickMe: function () {
      this.$emit('child-say', this.msg)
    }
  }
}
</script>
