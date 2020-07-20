<template>
    <div>
        <form @submit.prevent ="addTodo">

            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="submit" class="btn">
        </form>

    </div>
</template>

<script>
//import uuid from 'uuid';//npm install uuid, generates unique id
export default {
    name:"AddTodo",

    data() {
        return {
            title:''
        }
    },

    methods:{
        addTodo() {
                
           //e.preventDefault();//prevents the form try to submit to a file, 
            //stops default behavior
            const newTodo ={
              
                title: this.title,
                completed: false
            }
            //send up to parent by emiting event
            this.$emit('add-todo', newTodo);

            this.title =''; //to clear the form 
        }
    }

}
</script>

<style scoped>
form{
    display:flex;
}
inpt[type="text"]{
    flex:10;
    padding: 5px;
}
input[type="submit"] {
    flex:2;


}
</style>