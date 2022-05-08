<template>
  <h1>Jobs</h1>

  <div v-if="jobs.length">
    <div v-for="job in jobs" :key="job.id" class="job">  
      <router-link :to="{ name: 'JobDetails', params: { id: job.id } }">
        <h2>{{ job.title }}</h2>
      </router-link>  
    </div>
  </div>
  <div v-else>
    <p>Loading jobs...</p>
  </div>

</template>

<script>
const URL_BASE = "http://localhost:3000/jobs";

export default {
    data() {
        return {
            jobs: []
        }
    }, 

    mounted(){
      fetch(URL_BASE, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      })
      .then(response => response.json())
      .then(json => {
        this.jobs = json;
      })
      .catch(error => console.error(error.message));
    },
}
</script>

<style>
  .job h2{
    background: #f4f4f4;
    padding: 20px;
    border-radius: 10px;
    margin: 10px auto;
    max-width: 600px;
    cursor: pointer;
    color: #444;
  }

  .job h2:hover{
    background: #ddd;
  }

  .job a{
    text-decoration: none;
  }
</style>