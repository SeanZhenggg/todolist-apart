<template>
    <div>
        <input type="text" v-model="NewTodo" v-on:keyup.enter="readyToAdd">
        <button v-on:click="readyToAdd">submit</button>
    </div>
</template>

<script>
export default {
    name:'InputTodo',
    data:function(){
        return{
        NewTodo:'',
        }
    },
    methods:{
        readyToAdd(event){
            event.preventDefault();
            let value = this.NewTodo.trim();
            if(!value) return;
            this.$emit('add:newtodo',value);
            this.NewTodo = '';
        }
    }
}
</script>

<style scoped>
</style>


