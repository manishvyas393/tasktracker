<template>
  <form class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="Text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input type="text" v-model="day" name="day" placeholder="Add Day&time" />
    </div>
    <div class="form-control">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="day" />
    </div>
    <input @click="onSubmit()" type="button" value="save-task" class="btn" />
  </form>
</template>
<script>
export default {
  name: "AddTask",
  data() {
    return {
      Text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit() {
      if (!this.Text) {
        alert("please add a task");
        return;
      }
      const newTask = {
        Text: this.Text,
        day: this.day,
        reminder: this.reminder,
      };
      this.$emit("add-task", newTask);

      this.Text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  display: flex;
  flex-direction: column;
}
.form-control {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
  width: 100%;
}
input {
  padding: 8px;
  margin-top: 5px;
}
</style>