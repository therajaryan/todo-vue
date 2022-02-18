<template>
    <div>
        <form>
            <input style="margin:auto; width: 220px; margin-bottom:10px; margin-top:50px;" v-model="gName" class="" type="text" placeholder="Group Name">
            <br>
            <button v-on:click.prevent="addGroup" style="margin:auto; margin-bottom:20px;">Add Group</button>
        </form>
        <div v-for="(g, index) in groups" :key="g.id" class="" >
            <div>
                <div v-if="!g.editing" @click="singleClick()" @dblclick="doubleClick(g)" class="">
                    {{parseInt(index)+1}}. &nbsp;&nbsp; {{g.title}}
                </div>
                <input v-else class="" type="text" v-model="g.title" @blur="doneEditG(g)" @keypress.enter="doneEditG(g)" @keyup.escape="cancelEditG(g)" v-focus>
            </div>
            <div class="remove-item" @click="$deleteG(index)">
                &times;
            </div>
        </div>
    </div>
</template>

<script>
let time = null;
export default {
    name: 'todo-group',
    data() {
        return{
            test: '',
            gName: '',
            idForGroup: 1,
            editCache: '',
            delay: 700,
            clicks: 0,
            timer: null,
            groups: [
            // {
            //   'id': 1,
            //   'title': 'Tech',
            //   'open': false,
            //   'editing': false,
            // }
            ],
        }
    },
    directives: {
        focus: {
          inserted: function (el) {
            el.focus()
          }
        }
    },
    methods: {
        
        singleClick(){
            // first clear  time
            clearTimeout(time);
            time = setTimeout(() => {
            console.log('single click')
            }, 400); 
            return this.openTodo();
        },
        doubleClick(g){
            clearTimeout(time);  
            console.log('double click');
            console.log(g);
            return this.editGroup(g);
        },
        openTodo(){

        },

        addGroup(){
            if(this.gName.trim().length == 0){
                return
            }
            this.groups.push({
              id: this.idForGroup,
              title: this.gName,
              open: false,
              editing: false,
            })
            this.gName = ''
            this.idForGroup++
        },
        
        $deleteG(index){
            this.groups.splice(index, 1)
        },

        editGroup(g){
            this.editCache = g.title
            g.editing = true
        },
        doneEditG(g) {
         if(g.title.trim().length == 0){
              g.title = this.editCache
            }
            g.editing = false
        },
        cancelEditG(g){
         g.title = this.editCache
         g.editing = false
        }
    },
}
</script>

<style>
    .remove-item {
      margin-right: 550px;
      margin-left: 15px;
      cursor: pointer;
    }
</style>