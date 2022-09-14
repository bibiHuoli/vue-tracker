<script>  
  import AddTask from '../components/AddTask.vue';
  import Tasks from '../components/Tasks.vue';

  export default {
    name: 'Home',
    components: {
      AddTask,
      Tasks,
    },
    props: {
      showAddTasks: Boolean,
    },
    data() {
      return {
        tasks: [],
      }
    },
    methods: {
      async fetchTasks() {
        const response = await fetch('api/tasks');
        const data = await response.json();
        return data;
      },
      async fetchTask(id) {
        const response = await fetch(`api/tasks/${id}`);
        const data = await response.json();
        return data;
      },
      async newTask(task) {
        const response = await fetch('api/tasks', {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(task),
        });
        const data = await response.json();

        this.tasks.push(data);
      },
      async deleteTask(id) {
        if(confirm('Are u sure?')) {
          const response = await fetch(`api/tasks/${id}`, {
            method: 'DELETE',
          });
          response.status === 200 ? 
            (this.tasks = this.tasks.filter(function(task) {
              if(task.id !== id) return task.id
            })) :
            alert('faiou a deletage')
        }
      },
      async onReminder(id) {
        const taskToToggle = await this.fetchTask(id);
        const updateTask = {
          ...taskToToggle,
          reminder: !taskToToggle.reminder,
        };
        const response = await fetch(`api/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(updateTask),
        });
        const data = await response.json();
        this.tasks.forEach(function(task) {
          if(task.id === id) {
            task.reminder = data.reminder
          }
        })
      },
    },
    async created() {
      this.tasks = await this.fetchTasks();
    },
  }
</script>

<template>
  <AddTask
    @new-task="newTask"
    v-if="showAddTasks"
  />
  <Tasks
    @delete-task="deleteTask"
    @toggle-reminder="onReminder"
    :tasks="tasks"
  />
</template>

<style>

</style>