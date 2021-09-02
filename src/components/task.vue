<template>
  <div @dblclick="$emit('toggleReminder',task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <div>
      <h3>{{ task.Text }}</h3>
      <p>{{ task.day }}</p>
    </div>
    <div>
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </div>
  </div>
</template>
<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>