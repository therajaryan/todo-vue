<template>
    <div>
        <form>
            <input style="margin:auto; width: 220px; margin-bottom:10px; margin-top:50px;" v-model="gName" class="" type="text" placeholder="Group Name">
            <br>
            <button v-on:click.prevent="addGroup" style="margin:auto; margin-bottom:20px;">Add Group</button>
        </form>
        <div v-for="g in groups" :key="g.id" class="" >
            <div>
                <div>
                    {{g.id}} &nbsp;&nbsp; {{g.name}}
                </div>
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
            idForGroup: '',
            groups: [
            // {
            //   'id': 1,
            //   'name': 'Tech',
            //   'open': false,
            // }
            ],
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
            })
        },
    },
}
</script>

<style>

</style>