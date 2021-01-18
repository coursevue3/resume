<template>
  <form
    class="card card-w30"
    @submit.prevent="submitHandler"
  >
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select
        id="type"
        v-model="type"
        name="type"
      >
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea
        id="value"
        v-model.trim="value"
        name="value"
        rows="3"
      ></textarea>
    </div>

    <button
      :disabled="!isValue"
      class="btn primary"
      type="submit"
    >Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppResumeForm',
  emits: {
    'add-resume'(value) {
      if (value) {
        return true;
      }

      console.warn('No value in \'add-resume\' emit');
      return false;
    },
  },
  data() {
    return {
      type: 'title',
      value: '',
    };
  },
  computed: {
    isValue() {
      return this.value.length > 3;
    },
  },
  methods: {
    async submitHandler() {
      if (this.isValue) {
        const formData = {
          type: this.type,
          value: this.value,
        };

        try {
          const response = await fetch('https://vue-resume-3a0c9-default-rtdb.firebaseio.com/resume.json', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify({
              type: this.type,
              value: this.value,
            }),
          });

          const firebaseData = await response.json();

          this.$emit('add-resume', {
            id: firebaseData.name,
            ...formData,
          });

          this.cleanForm();
        } catch (err) {
          console.warn(err);
        }
      }

      return;
    },

    cleanForm() {
      this.type = 'title';
      this.value = '';
    },
  },
};
</script>

<style scoped>

</style>
