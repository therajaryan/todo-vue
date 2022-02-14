<template>
  <div id="text">
       TASKS:
      <p></p>
      <input style="margin:auto; width: 220px;" type="text" class="todo-input" placeholder="What's up" v-model="message" @keypress.enter="addTodo" >
      <p></p>
      <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
          <!-- <span>Hello</span> -->
          <div>
            {{todo.id}}.&nbsp;&nbsp;{{todo.title}}
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
      idForTodo: 1,
      todos: [
          //{
            // 'id': 1,
            // 'title': 'Write todo',
            // 'completed': false,
          //}
      ]
    }
  },
  methods: {
      addTodo(){
        if(this.message.trim().length == 0){
          return
        }
          this.todos.push({
              id: this.idForTodo,
              title: this.message,
              completed: false,
          })
          // alert('adding')

          this.message = ''
          this.idForTodo++
      },
      $delete(index){
        this.todos.splice(index, 1)

        this.idForTodo--
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
        margin: 2px 0 20px 10px
        
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

    #text {
        margin-top: 20px;
        margin-bottom: 20px;
        font-size: 15px;
        padding-bottom: 20px;
    }
</style>
