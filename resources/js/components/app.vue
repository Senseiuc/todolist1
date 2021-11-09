<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form v-on:reload_list="getList()"></add-item-form>
        </div>
        <list-view :items="items" v-on:reload_list="getList()"></list-view>
    </div>
</template>

<script>
    export default {
        data: function (){
            return {
                items: []
            }
        },
        methods: {
            getList (){
                axios.get('api/item')
                    .then( response => {
                        this.items = response.data
                    })
                    .catch( error => {
                        console.log(error)
                    })
            }
        },

        created() {
            this.getList();
        }
    }
</script>

<style scoped>
.todoListContainer{
    width: 350px;
    margin: auto;
}
.heading{
    background:#e6e6e6 ;
    padding: 10px;
}
#title{
    text-align: center;

}
</style>
