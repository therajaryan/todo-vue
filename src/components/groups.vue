<template>
    <div>
        <form>
            <input style="margin:auto; width: 220px; margin-bottom:10px; margin-top:50px;" v-model="gName" class="" type="text" placeholder="Group Name">
            <br>
            <button v-on:click.prevent="addGroup" style="margin:auto; margin-bottom:20px;">Add Group</button>
        </form>
        <div v-for="(g, index) in groups" :key="g.id" class="" >
            <div>
                <div v-if="!g.editing" @dblclick="editGroup(g)" class="">
                    {{parseInt(index)+1}}. &nbsp;&nbsp; {{g.name}}
                </div>
                <input v-else class="" type="text" v-model="g.name" @blur="doneEditG(g)" @keypress.enter="doneEditG(g)" @keyup.escape="cancelEditG(g)" v-focus>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'todo-group',
    data() {
        return{
            gName: '',
            idForGroup: 1,
            editCache: '',
            groups: [
            // {
            //   'id': 1,
            //   'name': 'Tech',
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
        addGroup(){
            if(this.gName.trim().length == 0){
                return
            }
            this.groups.push({
              id: this.idForGroup,
              name: this.gName,
              open: false,
              editing: false,
            })
            this.gName = ''
            this.idForGroup++
        },
        
        $delete(index){
            this.g.splice(index, 1)
         },

        editGroup(g){
            this.editCache = g.name
            g.editing = true
        },
        doneEditG(g) {
         if(g.name.trim().length == 0){
              g.name = this.editCache
            }
            g.editing = false
        },
        cancelEditG(g){
         g.name = this.editCache
         g.editing = false
        }
    },
}
</script>

<style>

</style>