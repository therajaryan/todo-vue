<template>
  <div id="text">
       TASKS:
      <p></p>
      <form>
        <input style="margin:auto; width: 220px; margin-bottom:10px;" type="text" class="todo-input" placeholder="What's up" v-model="message">
        <input style="margin:auto; width: 220px; margin-bottom:10px;" type="date" class="todo-input" v-model="ddate" >
        <button v-on:click.prevent="addTodo" style="margin:auto; ">Add</button>
      </form>
      <div style="margin-top: 10px;">
        <button v-on:click.prevent="sortDate">Sort by Date</button>
      </div>
      <p></p>
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
          <div class="todo-item-left">
            <input type="checkbox" v-model="todo.completed">
            <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label" :class="{check: todo.completed}" >
              {{parseInt(index)+1}}.&nbsp;&nbsp;{{todo.title}}&nbsp;&nbsp;&nbsp;&nbsp;{{todo.date}}
            </div>
            <input v-else class="todo-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keypress.enter="doneEdit(todo)" @keyup.escape="cancelEdit(todo)" v-focus>
          </div>
        <div class="remove-item" @click="$delete(index)">
          &times;
       </div>
     </div>
  </div>
</template>

<script>
export default {
  name: 'todo-list', 
  data () { 
    return {
      message: '',
      ddate: '',
      idForTodo: 1,
      counter: 1,
      editCache: '',
      todos: [
          //{
            // 'id': 1,
            // 'title': 'Write todo',
            // 'completed': false,
          //}
      ]
    }
  },
  // computed: {
  //   fullTask: {
  //     get(){
  //       return this.message;
  //     },
  //   }
  // },
  directives: {
    focus: {
    // directive definition
      inserted: function (el) {
        el.focus()
     }
    }
  },
  methods: {
      sortDate(){
        var x = this.todos.sort((a, b) => new Date(a.date) - new Date(b.date))
        console.log(x)
        return x
      },
      addTodo(){
        if(this.message.trim().length == 0){
          return
        }
          this.todos.push({
              id: this.idForTodo,
              title: this.message,
              completed: false,
              editing: false,
              date: this.ddate,
          })
          // alert('adding')
          this.ddate = ''
          this.message = ''
          this.idForTodo++
          counter++
      },
      $delete(index){
        this.todos.splice(index, 1)
      },
      editTodo(todo){
        this.editCache = todo.title
        todo.editing = true
      },
      doneEdit(todo) {
        if(todo.title.trim().length == 0){
          todo.title = this.editCache
        }
        todo.editing = false
      },
      cancelEdit(todo){
        todo.title = this.editCache
        todo.editing = false
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

    .todo-input {
        /* height: 20px; */
        /* max-width: 250px; */
        padding: 10px 18px;
        display: block;
        border: solid 1px #aacfe4;
        width: 150px;
        margin: 2px 0 20px 10px;
        color: #2c3e50;
        font-size: 15px;
    }
    .todo-item {
      /* text-align: left; */
      margin-left: 41%;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      
    }
    .remove-item {
      margin-right: 550px;
      margin-left: 15px;
      cursor: pointer;
    }
    .todo-edit {
      font-size: 15px;
      border: solid 1px white;
      margin-left: 12px;
      width: 100%;
      color: #2c3e50;
      padding: 10px;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
    }
    .todo-item-label{
      padding: 10px;
      border: 1px solid white;
      margin-left: 12px;
    }
    .todo-item-left{
      display: flex;
      align-items: center;
    }
    .check{
      text-decoration: line-through;
      color: grey;
    }
    #text {
        margin-top: 20px;
        margin-bottom: 20px;
        font-size: 15px;
        padding-bottom: 20px;
    }
</style>
