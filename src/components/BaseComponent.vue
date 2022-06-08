<template>
  <div>
    <h2>
      Child component
    </h2>
    <div class="box" />
  </div>
</template>

<script>
export default {
  name: 'BaseComponent',
}
</script>

<style scoped>
.box {
  background: red;
  width: 50px;
  height: 50px;
}
</style>
