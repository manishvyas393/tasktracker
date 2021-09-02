<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @onclick="$emit('toggle-add-task')"
      :text="show ? 'Close' : 'AddTask'"
      :color="show ? 'red' : 'green'"
    />
  </header>
</template>
<script>
import Button from "./button.vue";

export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Task Tracker",
    },
    show: Boolean,
  },
  components: {
    Button,
  },
};
</script>
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>