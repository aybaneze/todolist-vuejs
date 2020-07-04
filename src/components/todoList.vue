<template>
  <form id="app" @submit.prevent="createTask">
    <div>
      <label class="label" for="task">Nueva Lista de compras</label>
      <fieldset>
        <input type="text" v-model="newTask" id="task" />
        <input type="submit" class="btn-add" value="CREAR" />
      </fieldset>
    </div>

    <ul class="tasks">
      <li v-for="(task, i) in tasks" :key="'task' + i" :class="{completed: task.completed}">
        <input type="checkbox" @click="completeTask(task, i)" :checked="task.completed" />
        {{task.text}}
        <button
          @click="removeTask(task)"
          type="button"
          class="btn-delete"
          name="button"
        >x</button>
      </li>
    </ul>
  </form>
</template>

<script>
export default {
  data: () => ({
    newTask: "",
    tasks: []
  }),
  methods: {
    createTask(e) {
      let task = {
        id: e,
        text: this.newTask,
        completed: false
      };
      if (this.newTask !== "") {
        this.tasks.push(task);
        this.newTask = "";
      }
      console.log(this.tasks);
    },
    completeTask(task, e) {
      //  console.log(e);
      const taskIndex = this.tasks.indexOf(task);
      for (let i = 0; i < this.tasks.length; i++) {
        let task = this.tasks[i];
        if (!this.tasks[taskIndex].completed) {
          this.tasks[taskIndex].completed = true;
        } else {
          this.tasks[taskIndex].completed = false;
        }

        console.log(task.completed, e);
      }
    },
    removeTask(task) {
      const taskIndex = this.tasks.indexOf(task);
      this.tasks.splice(taskIndex, 1);
    }
  }
};
</script>

<style scoped>
body {
  height: 100%;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.completed {
  text-decoration: line-through;
  color: grey;
}
#app div {/* fallback for old browsers */
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  flex-direction: column;
  width: 50%;
  padding: 20px;
  border: 1px solid #d4d4d4;
  border-radius: 5px;
}
#app form {
  width: 100%;
}
.label {
  font-size: 18px;
  font-weight: bold;
}
fieldset {
  border: none;
  margin: 15px;
  display: flex;
  flex-direction: column;
  justify-content: right;
}
#task {
  height: 50px;
  width: 300px;
}
.btn-add {
  border-radius: 5px;
  width: 80px;
  height: 30px;
  line-height: 1.5;
  border: none;
  color: #fff;
  background: #00779b; /* fallback for old browsers */
  font-size: 12px;
  margin: 10px 0 0 auto;
  font-weight: bold;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
.btn-add:hover{
   background: #004458; 
   cursor: pointer;
}

ul.tasks {
  width: 100%;
  margin: auto;
  padding: 0;
}
.tasks li {
  list-style: none;
  border: 1px solid #d4d4d4;
  padding: 20px;
  width: 50%;
  margin: 10px auto 15px;
  position: relative;
  border-radius: 5px;
-webkit-box-shadow: 4px 11px 24px -19px rgba(0,0,0,0.75);
-moz-box-shadow: 4px 11px 24px -19px rgba(0,0,0,0.75);
box-shadow: 4px 11px 24px -19px rgba(0,0,0,0.75);
}
.tasks li input {
  position: absolute;
  left: 20px;
}
.tasks li .btn-delete {
  position: absolute;
  right: 20px;
  background: #00779b;
  color: #fff;
  border: none;
  border-radius: 5px;
}
@media (max-width: 700px) {
  #app div {
    width: 95%;
  }
  ul.tasks {
    width: 95%;
    margin: auto;
    padding: 0; 
  }
}
</style>