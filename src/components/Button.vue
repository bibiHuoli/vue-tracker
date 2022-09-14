<script>
  export default {
    name: 'Button',
    props: {
      background: String,
      text: String,
    },
    emits: [
      'btn-click',
    ],
    methods: {
      onClick() {
        this.$emit('btn-click');
      },
    },
  }
</script>

<template>
  <button
    @click="onClick()"
    class="btn"
    :style= "{ backgroundColor: background }"
  >
    {{ text }}
  </button>
</template>