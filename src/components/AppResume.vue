<template>
  <app-resume-form @add-resume="addResume"></app-resume-form>
  <app-resume-list :resume="resume"></app-resume-list>
</template>

<script>
import AppResumeForm from '@/components/AppResumeForm.vue';
import AppResumeList from '@/components/AppResumeList';

export default {
  name: 'AppResume',
  components: {
    AppResumeForm,
    AppResumeList,
  },
  data() {
    return {
      resumeList: [],
    };
  },
  created() {
    this.getResume();
  },
  computed: {
    resume() {
      return this.resumeList;
    },
  },
  methods: {
    addResume(value) {
      this.resumeList.push(value);
    },
    async getResume() {
      try {
        const data = await fetch('https://vue-resume-3a0c9-default-rtdb.firebaseio.com/resume.json');
        const res = await data.json() || {};

        this.resumeList = Object.keys(res).map(key => {
          return {
            id: key,
            ...res[key],
          };
        });
      } catch (err) {
        console.warn(err);
      }
    },
  },
};
</script>

<style scoped>

</style>
