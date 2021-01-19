<template>
  <p v-if="commentsList.length === 0">
    <button
      class="btn primary"
      @click="getComments"
    >Загрузить комментарии</button>
  </p>
  <div
    v-else
    class="card"
  >
    <h2>Комментарии</h2>
    <app-comments-list :comments="comments"></app-comments-list>
  </div>
  <div
    v-if="loading"
    class="loader"
  ></div>
</template>

<script>
import AppCommentsList from '@/components/AppCommentsList';

export default {
  name: 'AppComments',
  components: {
    AppCommentsList,
  },
  data() {
    return {
      commentsList: [],
      loading: false,
    };
  },
  computed: {
    comments() {
      return this.commentsList;
    },
  },
  methods: {
    async getComments() {
      this.loading = true;

      try {
        const data = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=5');
        const res = await data.json() || {};

        this.commentsList = Object.keys(res).map(key => {
          return {
            ...res[key],
          };
        });
      } catch (err) {
        console.warn(err);
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<style scoped>

</style>
