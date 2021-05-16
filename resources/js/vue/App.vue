<template>
   <div class="toListcontainer">
        <div>
            <h2>It is a Tolist</h2>
            <AddItem  :items="items" v-on:reloadList="getList()"/>
        </div>
 
    <listItems :items="items" v-on:reloadList="getList()"/>
    </div>


</template>

<script>
import AddItem from './addItem.vue';
import listItems from './listItems.vue';
export default {
    components: {
        AddItem,
        listItems
    },
 data() {
     return {
         items:[]
     }
 },
 methods: {
     getList(){
         axios.get('api/items')
         .then(res => {
             this.items=res.data
         })
         .catch(err => {
             console.error(err); 
         })
     }
     
 },

     created() {
         this.getList();
     },     
   
}
</script>

<style scoped>
    .toListcontainer{
        display: flex;
        width: 100%;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-color: #fafafc;
    }
    h2{
        font-size: 2rem;
    }
</style>