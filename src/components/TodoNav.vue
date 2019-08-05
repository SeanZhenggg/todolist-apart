<template>
    <div>
        <ul>
            <li><a href="#" :class="{'active' : Visibility == 'all'}" @click.prevent="Visibility = 'all';showView(Visibility);">ALL</a></li>
            <li><a href="#" :class="{'active' : Visibility == 'ing'}" @click.prevent="Visibility = 'ing';showView(Visibility);">UNDO</a></li>
            <li><a href="#" :class="{'active' : Visibility == 'done'}" @click.prevent="Visibility = 'done';showView(Visibility);">DONE</a></li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'TodoNav',
    data:function(){
        return{
            Visibility:'all',
        }
    },
    methods:{
        showView(vis){
           this.$emit('show:view',vis);
        }
    }
}
</script>

<style scoped>
    ul{
        list-style-type: none;
        padding:0;
    }
    li{
        background-color:#BBBBBB;
        display:inline-block;
        width:100px;
    }
    a{
        padding:20px 30px;
        display:block;
        text-decoration: none;
        color:black;
    }
    a:hover{
        background:#444444; 
    }
    .active{
        background:#444444;
    }
</style>


