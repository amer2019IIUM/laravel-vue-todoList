<template>
    <div class="addItem">
      
        <input type="text" class="inputForm" aria-label="input Item" aria-describedby="input Item" placeholder="Type your todo item" v-model="item.name">
        <font-awesome-icon  icon="plus-square" :class="[item.name ? 'active' : 'inactive', 'plus']" @click="addItem()" />
    
    </div>

</template>
<script>
export default {
   data() {
       return {
           item:{
               'name':""
           }
       }
   },
   methods: {
       addItem(){
           if(this.item.name==''){
               return ''
           }
           axios.post('api/item/store',{
               item:this.item
           })
           .then(res => {
             if(res.status==201){
                 this.item.name=''
                  this.$emit('reloadList')
             }
           })
           .catch(err => {
               console.error(err); 
           })

       }
   },
     
}
</script>

<style scoped>
 .addItem{
     display: flex;
     justify-content: center;
     align-items: center;
 }
 input{
     background: #f7f7f7;
     border: 0px;
     outline: 5px;
     padding: 5px;
     margin-right: 10px;
     width: 100%;
 }
 .plus{
     font-size: 20px;
 }
 .active{
     color: aqua;
 }
 .inactive{
     color: #9999;
 }
</style>