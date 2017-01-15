<template>
  <div class="hello">
    <hr>
    <h1>下面为子组件内容</h1>
    <h1><a href="#">{{ msg }}</a></h1>
    <h1><a href="#">{{ msgfromfather }}</a></h1>
     <input v-model="msgtodad">  
    <button v-on:click="saySomthing">子对父说</button>   
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Hello from Component A',
      msgtodad: ''
    }
  },
  props: ['msgfromfather'],
  methods: {
        saySomthing: function() {
          this.$emit('child-says-something', this.msgtodad);
        }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
