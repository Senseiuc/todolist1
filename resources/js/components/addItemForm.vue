<template>
    <div class="addItem">
        <input type="text" v-model="items.name">
        <font-awesome-icon
            icon = "plus-square"
            :class="[items.name ? 'active' : 'inactive' , 'plus']"
            @click="addItem()"
            />

    </div>
</template>

<script>
    export default {
        data: function (){
            return {
                items: {
                    name:""
                }
            }
        },

        methods:{
            addItem(){
                if (this.items.name === ''){
                    return
                }
                axios.post('/api/item/store', {
                    item: this.items
                })
                .then( response => {
                    if (response.status === 201){
                        this.items.name = "";
                        this.$emit('reload_list')
                    }
                })
                .catch(error => {
                    console.log(error)
                })
            }
        }
    }
</script>

<style scoped>
.addItem{
    display: flex;
    justify-content: center;
    align-items: center;
}
input{
    background: #f7f7f7 ;
    border: 0;
    outline: none;
    padding: 5px;
    margin: 10px;
    width: 100%;
}

.plus {
    font-size: 20px;
}
.active {
    color: #00ce25;
}
.inactive{
    color: #999999;
}
</style>
