<template>
    <div v-if="job">
        <h1>{{ job.title }}</h1>
        <p>The job id {{ id }}</p>
        <p>The job id {{ job.details }}</p>
    </div>
    <div v-else>
        <p>Loading job detail...</p>
    </div>
</template>

<script>

const URL_BASE = "http://localhost:3000/jobs/";

export default {
    props: ['id'],

    data(){
        return {
            job: null,
        }
    },

    mounted(){
      fetch(URL_BASE + this.id, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      })
      .then(response => response.json())
      .then(json => {this.job = json;})
      .catch(error => console.error(error.message));
    },

    /*data(){
        return {
            job: {
                id: this.$route.params.id,
            },
        }
    },*/
}
</script>

<style>

</style>