<template>
  <p>{{ value }}</p>
</template>

<script>
export default {
  name: 'AppResumeText',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>

</style>
