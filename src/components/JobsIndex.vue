<template>
  <main class="JobsIndex">
    <h1>See All Jobs</h1>
    <form class="JobsIndex-filter" id="job-filters">
      <label class="JobsIndex-label" for="skill-filter">Filter By Skills</label>
      <input class="JobsIndex-input" id="skill-filter" name="skill-filter" type="text">
    </form>
    <button>Create Job</button>
    <component
      v-for="job in jobs"
      v-bind:key="job.id"
      v-bind:job="job"
      v-bind:is="job.view">
    </component>
  </main>
</template>

<script>
import { getJobList } from '../helpers/jobsApiHelper';
import ShowJob from './ShowJob';
import EditJob from './EditJob';
export default {
  name: 'JobsIndex',
  components: {
    ShowJob,
    EditJob
  },
  data: function () {
    return {
      jobs: [],
      jobView: this.getJobView
    }
  },
  mounted: async function () {
    let jobs = await getJobList();
    this.jobs = jobs.map((job) => {
      job.view = ShowJob;
      return job;
    })
  }
}
</script>

<style scoped lang="scss">
  .JobsIndex {
    &-label {
      margin-right: 8px;
      font-weight: 600;
    }
  }  
</style>
