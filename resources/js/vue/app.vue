<template>
    <div class="todContainer">
        <div class="heading">
            <h2 id="title">To do list</h2>
            <addItemForm v-on:reloadList="getList()"></addItemForm>
        </div>
        <listView :items="items"  v-on:reloadList="getList()"/>

    </div>
</template>
<script>
import axios from 'axios'
import addItemForm from './addItemForm.vue'
import listView from './listView.vue'


export default {
    components: {
        addItemForm, listView
    },
    data:function(){
        return{
            items:[]
        }
    },
    methods: {
        getList(){
            axios('api/items/').then(response=>{
                this.items=response.data
            }).catch(error=>{
                console.log(error);
            })
        }
        
    },
    created(){
        this.getList();
    }
}
</script>
<style scoped>
.todContainer {
    width: 350px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;
}

#title {
    text-align: centre;
}
</style>