<template>
  <form class="EditJob" @submit.prevent>
    <div class="EditJob-control">
      <label class="EditJob-label" for="title">Job Title</label>
      <input v-model="jobData.title" type="text" class="EditJob-input" name="title">
    </div>
    <div class="EditJob-control">
      <label class="EditJob-label" for="descripiton">Job Description</label>
      <input v-model="jobData.description" type="text" class="EditJob-input" name="description">
    </div>
    <div class="EditJob-control">
      <label class="EditJob-label" for="skills">Skills</label>
      <input v-for="(skill, index) in jobData.skills" v-bind:key="index" v-model="jobData.skills[index]" type="text" class="EditJob-input" name="skills">
      <input v-model.lazy="jobData.skills[jobData.skills.length]" type="text" class="EditJobs-input" name="skills">
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
      jobData: {
        id: this.job.id,
        title: this.job.title,
        description: this.job.description,
        skills: this.job.skills
      }
    }
  },
  methods: {
    closeForm: function () {
      this.job.view = 'ShowJob';
      this.$emit('cancel')
    },
    submitForm: function () {
      this.$emit('job-saved', this.jobData);
    }
  }
}
</script>

<style scoped lang="scss">
</style>