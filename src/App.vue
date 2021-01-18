<template>
  <div class="container column">
    <app-resume></app-resume>
  </div>

  <div class="container">
    <app-comments></app-comments>
  </div>
</template>

<script>
import AppResume from '@/components/AppResume';
import AppComments from '@/components/AppComments';

export default {
  name: 'App',
  components: {
    AppResume,
    AppComments,
  },
};
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
