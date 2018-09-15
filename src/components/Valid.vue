<template>
    <div class="forms">
        <h1>{{ msg }}</h1>

        <button id="addTask" v-on:click="addTask">Add</button>
        <input
                name="tasks"
                type="text"
                id="taskName"
                v-validate="'required|min:3'"
        >
        <div v-show="errors.has('tasks')">
            {{ errors.first('tasks') }}
        </div>
        <li v-for="(task, index) in tasks">
            <span>{{task.name}}</span>
            <button v-on:click="deleteTask(index)"> usuń </button>
        </li>
    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data() {
            return {
                greeting: 'Hello Vue!',
                tasks: [{
                    name: 'Task 1'
                }, {
                    name: 'Task 2'
                }]
            }
        }
        ,
        methods: {
            addTask: function () {
                this.$validator.validateAll().then(result => {
                    if (!result) {
                        return;
                    }
                    let taskName = document.querySelector('#taskName');
                    this.tasks.push({name: taskName.value});
                    taskName.value = "";
                });
            }
            ,
            deleteTask: function (index) {
                this.tasks.splice(index, 1);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .forms {
        float: left;
    }
</style>
