<template>
  <div>
    <h1>
      First Component
    </h1>
    <p>
      Parent Message: {{ parentMessage }}
    </p>
    <p>
      Parent number: {{ parentNumber }}
    </p>
    <slot name="header" number="10" />
    <p>
      {{ number }}
    </p>
    <p>
      {{ message }}
    </p>
    <slot name="footer" />
    <button @click="$emit('myFirstEmit', { firstName: 'Denis', age: 20 })">
      Click me to emit an event
    </button>
  </div>
</template>

<script>
  export default {
    name: 'FirstComponent',
    props: {
      parentMessage: String,
      parentNumber: Number,
    },
    emits: ['myFirstEmit'],
    data () {
      return {
        number: 1,
        message: 'My First Component'
      }
    }
  }
</script>

<style scoped>
  * {
    color: green;
  }
</style>