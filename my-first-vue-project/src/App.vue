<template>
  <div id="app">
      <!-- <h1>{{title}}</h1> -->
      <!-- <h1 v-text="title"></h1> -->
      <h1>父组件内容</h1>
      <h1 v-html="title"></h1>
      <input v-model="newItem" v-on:keyup.enter="addNew">
      <ul>
        <li v-for="item,index in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
            {{item.label}}
            <!-- <span v-if="item.isFinished">Y</span>
            <span v-if="!item.isFinished">N</span> -->
        </li>
      </ul>
      父对子说: <input v-model="msgfromfather">
      <h1>Son's Words: {{wordsfromson}}</h1>
      <component-a v-bind:msgfromfather="msgfromfather" v-on:child-says-something="listenToSon"></component-a>      
  </div>
</template>

<script>
import Store from "./store"
import componentA from "./components/componentA"

export default {
  data: function() {
    return {
      title: 'this is a todo list<em>!</em>',
      items: Store.fetch(),      
      newItem: '',
      wordsfromson: '',
      msgfromfather:''
     } 
  },
  methods: {
    toggleFinish: function(item) {
      console.log(item);
      item.isFinished = !item.isFinished;
    },
    addNew: function() {
      // alert(this.newItem);
      this.items.push({label:this.newItem, isFinished: false} );
      this.newItem='';
    },
    listenToSon: function(childsWords) {
      console.log(childsWords);
      this.wordsfromson = childsWords;
    },    
  },
  watch: {
      items: {
          handler: function() {Store.save(this.items)},
          deep: true
      }
  },
  components: {componentA}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /*margin-top: 60px; */
  margin: 60px auto; 
  width: 800px;
}

#app ul {
  list-style: none;
}

.finished {
  text-decoration: underline;
}
</style>
