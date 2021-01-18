<template>
  <ul class="list">
    <li
      v-for="comment in comments"
      :key="comment.id"
      class="list-item"
    >
      <div>
        <p><strong>{{ comment.email }}</strong></p>
        <small>{{ comment.body }}</small>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'AppCommentsList',
  props: {
    comments: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>

</style>
