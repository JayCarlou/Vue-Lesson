<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add todo..." required>
            <input type="submit" value="submit" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: "AddTodo",
    data(){
        return{
            title: ''
        }
    },
    methods: {
        addTodo(e){
            // alert("hello world");
            e.preventDefault();
            const newTodo = {
                id: 4,
                title: this.title,
                completed: false
            }

            //send via emit
            this.$emit('add-todo', newTodo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form{
        display: flex;
    }
    input[type="text"]{
        flex: 10;
        padding: 5px;
    }
    input[type="button"]{
        flex: 2;
    }

</style>