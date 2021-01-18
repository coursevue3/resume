<template>
  <div class="card card-w70">
    <template v-if="resume.length > 0">
      <component
        :is="`AppResume${capitalize(block.type)}`"
        v-for="block in resume"
        :key="block.id"
        :value="block.value"
      ></component>
    </template>
    <p v-else>Добавьте первый блок, чтобы увидеть результат</p>
  </div>
</template>

<script>
import AppResumeTitle from '@/components/AppResumeTitle';
import AppResumeSubtitle from '@/components/AppResumeSubtitle';
import AppResumeAvatar from '@/components/AppResumeAvatar';
import AppResumeText from '@/components/AppResumeText';

export default {
  name: 'AppResumeList',
  props: {
    resume: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  components: {
    AppResumeTitle,
    AppResumeSubtitle,
    AppResumeAvatar,
    AppResumeText,
  },
  methods: {
    capitalize(value) {
      if (!value) return '';
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
  },
};
</script>

<style scoped>

</style>
