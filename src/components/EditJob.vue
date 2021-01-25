<template>
  <form class="EditJob" @submit.prevent>
    <div class="EditJob-control">
      <label class="EditJob-label" for="title">Job Title</label>
      <input v-model="title" type="text" class="EditJob-input" name="title">
    </div>
    <div class="EditJob-control">
      <label class="EditJob-label" for="descripiton">Job Description</label>
      <input v-model="description" type="text" class="EditJob-input" name="description">
    </div>
    <div class="EditJob-control">
      <label class="EditJob-label" for="skills">Skills</label>
      <input v-for="(skill, index) in job.skills" v-bind:key="index" v-model="skills[index]" type="text" class="EditJob-input" name="skills">
      <input v-model.lazy="skills[skills.length]" type="text" class="EditJobs-input" name="skills">
    </div>
    <input type="submit" class="EditJob-submit" value="Save" @click="submitForm()">
    <button class="EditJob-close" @click="closeForm()" type="button">Cancel</button>
  </form>
</template>

<script>
export default {
  name: 'EditJob',
  props: {
    job: {
      default: function () {
        return {
          title: '',
          skills: [],
          description: ''
        }
      },
      type: Object
    }
  },
  data: function () {
    return {
      title: this.job.title,
      description: this.job.description,
      skills: this.job.skills
    }
  },
  methods: {
    closeForm: function () {
      this.job.view = 'ShowJob';
      this.$emit('cancel')
    },
    submitForm: function () {
      this.$emit('job-saved', this.job);
    }
  }
}
</script>

<style scoped lang="scss">
</style>