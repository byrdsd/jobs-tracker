<template>
  <div class="ShowJob">
    <h2 class="ShowJob-heading">
      {{ job.title }}
    </h2>
    <p class="ShowJob-description">
      {{ job.description }}
    </p>
    <ul class="ShowJob-skills">
      <li v-for="skill in job.skills" :key="skill" class="ShowJob-skill">
        {{ skill }}
      </li>
    </ul>
    <button v-on:click="editView(job)" class="ShowJob-control">
      Edit
    </button>
    <button @click="$emit('delete', job)" class="ShowJob-control">
      Delete
    </button>
  </div>
</template>

<script>
export default {
  name: 'ShowJob',
  props: {
    job: Object
  },
  methods: {
    editView: function (job) {
      job.view = 'EditJob';
    }
  }
}
</script>