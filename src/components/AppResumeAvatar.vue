<template>
  <div class="avatar">
    <img :src="value">
  </div>
</template>

<script>
export default {
  name: 'AppResumeAvatar',
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
