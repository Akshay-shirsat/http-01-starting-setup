<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences">Load Submitted Experiences</base-button>
      </div>
      
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :id="result.id"
          :name="result.name"
          :rating="result.rating"
          
        ></survey-result>
      </ul>

    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';

export default {
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
     
    };
  },
  methods: {
    loadExperiences() {
      fetch('https://vue-http-demo-25b46-default-rtdb.firebaseio.com/surveys.json')
        .then((res) => {
          if (res.ok) {
            return res.json();
          }
        })
        .then((data) => {
          const results = [];
          for (const id in data) {
            results.push({
              id: id,
              name: data[id].name,
              rating: data[id].rating,
            });
          }
          this.results = results;
        });
    },

    editExperience(id) {
      
      this.outputMessage = `Editing experience with ID: ${id}`;
    },

    confirmDelete(id) {
      const isConfirmed = confirm('Are you sure you want to delete this experience?');
      if (isConfirmed) {
        // Implement your logic for confirming and deleting the experience here
        // For example, make a DELETE request to the server
        this.outputMessage = `Confirmed deletion for experience with ID: ${id}`;
      } else {
        this.outputMessage = 'Deletion canceled.';
      }
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
