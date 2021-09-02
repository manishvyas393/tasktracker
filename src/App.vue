<template>
  <div class="container">
    <Header @toggle-add-task="toggleTask()" :show="show" />
    <div v-show="show">
      <AddTask @add-task="addtask" />
    </div>

    <Tasks
      @togleReminder="TogleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/header";
import AddTask from "./components/addtask";
import Tasks from "./components/tasks";
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      show: false,
    };
  },
  methods: {
    toggleTask() {
      this.show = !this.show;
    },
    async addtask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("eror");
      }
    },
    TogleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: poppins;
}
.fas {
  color: red;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid black;
  padding: 30px;
  border-radius: 5px;
  background-color: rgb(233, 233, 233);
}
.btn {
  color: white;
  background-color: black;
  padding: 8px;
  border: none;
  border-radius: 10px;
  text-transform: capitalize;
  font-size: 14px;
  font: bold;
}
.task {
  margin: 10px 20px;
  background: rgb(179, 175, 175);
  padding: 10px 5px;
  cursor: pointer;
  display: flex;
  text-transform: capitalize;
  justify-content: space-between;
}
.reminder {
  border-left: 5px solid blue;
}
</style>
