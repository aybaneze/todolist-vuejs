<template>
    <form id="app" @submit.prevent="createTask">
        <label class="label" for="task">Nueva Lista de compras</label>
        <input type="text" v-model="newTask" id="task">
        {{newTask}}
        <input type="submit" value="crear tarea">
        <ul>
            <li v-for="(task, i) in tasks" :key="'task' + i"  :class="{completed: task.completed}" >
                {{task.text}}<input type="checkbox" @click="completeTask(task.text, i)"  :checked="task.completed" />
                <button @click="removeTask(task)" type="button" name="button">x</button>
            </li>
        </ul>
    </form>
</template>

<script>
    export default{
        data: () =>({
            newTask: "",
            tasks: []
        }),
        methods:{
            createTask(e){
                let task = {
                    id: e,
                    text: this.newTask,
                    completed: true
                };
                this.tasks.push(task);
                this.newTask = "";
                console.log(this.tasks);
            },
             completeTask(taskText, e) {
                //  console.log(e);
                for (let i = 0; i < this.tasks.length; i++) {
                    let task = this.tasks[i];
                 
                        if (taskText === task.text) {
                        task.completed = !task.completed;
                           console.log(task.completed, e)
                    }
                }
            },
            removeTask(task){
                const taskIndex = this.tasks.indexOf(task);
                this.tasks.splice(taskIndex, 1);
            }
        }
    };
</script>

<style scoped>
    .completed {
        text-decoration: line-through;
        color: grey;
    }
</style>