<script>
  export default {
    name: 'Task',
    props: {
      task: Object,
    },
    methods: {
      onDelete(id) {
        this.$emit('delete-task', id)
      },
      onReminder(id) {
        this.$emit('toggle-reminder', id)
      }
    },
  }
</script>

<template>
  <div
    @dblclick="onReminder(task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fa fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<style scoped>
  .task {
    background-color: #f4f4f4;
    cursor: pointer;
    margin: 5px;
    padding: 10px 20px;
  }
  .reminder {
    border-left: 5px solid #0c0;
  }
  .task h3 {
    display: flex;
    place-content: space-between;
    place-items: center;
  }
  .fa {
    color: #a00;
  }
</style>