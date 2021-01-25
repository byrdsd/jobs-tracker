<template>
  <main class="JobsIndex">
    <h1>See All Jobs</h1>
    <form class="JobsIndex-filter" id="job-filters">
      <label class="JobsIndex-label" for="skill-filter">Filter By Skills</label>
      <input class="JobsIndex-input" id="skill-filter" name="skill-filter" type="text">
    </form>
    <button @click="newJob">Create Job</button>
    <component
      v-for="job in jobs"
      v-bind:key="job.id"
      v-bind:job="job"
      v-bind:is="job.view"
      @job-saved="saveJob"
      @delete="deleteJob">
    </component>
    <div v-if="showModal" class="JobsIndex-modal">
      <EditJob
        @cancel="closeModal"
        @job-saved="saveJob" />
    </div>
  </main>
</template>

<script>
import { getJobList, updateJob, createJob, destroyJob } from '../helpers/jobsApiHelper';
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
      showModal: false
    }
  },
  mounted: async function () {
    await this.updateJobs();
  },
  methods: {
    updateJobs: async function () {
      let jobs = await getJobList();
      this.jobs = jobs.map((job) => {
        job.view = ShowJob;
        return job;
      })
    },
    newJob: function () {
      this.showModal = true;
    },
    closeModal: function () {
      this.showModal = false;
    },
    saveJob: async function (job) {
      await (job.id ? updateJob(job) : createJob(job))
        .then(() => {
          job.view = ShowJob;
          this.updateJobs();
          this.closeModal();
        }, (error) => {
          console.error(error);
        });
    },
    deleteJob: async function (job) {
      await destroyJob(job.id)
        .then(() => {
          this.updateJobs();
        })
    }
  }
}
</script>

<style scoped lang="scss">
  .JobsIndex {
    &-label {
      margin-right: 8px;
      font-weight: 600;
    }

    &-modal {
      position: absolute;
      background-color: #fff;
      top: 100px;
      left: 0;
      right: 0;
      width: 80%;
      margin: auto;
      box-shadow: 0 4px 16px rgba(0,0,0,.3);
      padding: 20px;
    }
  }  
</style>
