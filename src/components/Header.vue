<script>
  import Button from './Button.vue';

  export default {
    name: 'Header',
    props: {
      showTasks: Boolean,
      title: String,
    },
    components: {
      Button,
    },
    computed: {
      homePage() {
        return this.$route.path === '/' ? true : false
      },
    },
    emits: [
      'toggle-add-tasks',
    ]
  }
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button 
      @btn-click="$emit('toggle-add-tasks')"
      :background='showTasks ? "#a00" : "#0c0"'
      :text="showTasks ? 'close rola' : 'add rola'"
      v-show="homePage"
    />
  </header>
</template>

<style scoped>
  header {
    display: flex;
    margin-bottom: 20px;
    place-content: space-between;
    place-items: center;
  }
</style>