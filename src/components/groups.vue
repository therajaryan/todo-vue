<template>
    <div>
        <form>
            <input style="margin:auto; width: 220px; margin-bottom:10px; margin-top:50px;" v-model="gName" class="" type="text" placeholder="Group Name">
            <br>
            <button v-on:click.prevent="addGroup" style="margin:auto; margin-bottom:20px;">Add Group</button>
        </form>
    </div>
</template>


<script>

export default {
    name: 'todo-group',
    data() {
        return{
            gName: '',
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

        },
    },
}
</script>

<style>

</style>