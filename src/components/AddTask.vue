<script>
  export default {
    name: 'AddTask',
    data() {
      return {
        text: '',
        day: '',
        reminder: false,
      }
    },
    methods: {
      onSubmit(e) {
        e.preventDefault()
        if(!this.text) {
          alert('Please add a task');
          return
        };
        const newTask = {
          text: this.text,
          day: this.day,
          reminder: this.reminder,
        };
        this.$emit('new-task', newTask);

        this.text = '';
        this.day = '';
        this.reminder = false;
      }
    },
    emits: [
      'new-task',
    ]
  }
</script>

<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input
        name="text"
        type="text"
        v-model="text"
        placeholder="Add Task"
      />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        name="day"
        type="text"
        v-model="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input
        name="reminder"
        type="checkbox"
        v-model="reminder"
      />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<style scoped>
  .add-form {
    margin-bottom: 40px;
  }
  .form-control {
    margin: 20px 0;
  }
  .form-control label {
    display: block;
  }
  .form-control input {
    font-size: 17px;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    width: 100%;
  }
  .form-control-check {
    display: flex;
    place-content: space-between;
    place-items: center;
  }
  .form-control-check label {
    flex: 1;
  }
  .form-control-check input {
    flex: 2;
    height: 20px;
  }
</style>