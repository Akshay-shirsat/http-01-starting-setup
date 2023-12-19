<template>
  <li>
    <div v-if="id === editingId">
      <!-- ... (editing UI) -->
    </div>
    <div v-else>
      <p>
        <span class="highlight">{{ name }}</span> rated the learning experience
        <span :class="ratingClass">{{ rating }}</span>.
      </p>
      <div>
        <base-button @click="editExperience">Edit</base-button>
        <base-button @click="confirmDelete">Delete</base-button>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  props: ['id', 'name', 'rating'],
  computed: {
    ratingClass() {
      return 'highlight rating--' + this.rating;
    },
  },
  data() {
    return {
      editingId: null,
      editedName: this.name,
      editedRating: this.rating,
    };
  },
  methods: {
  editExperience() {
    console.log('Edit experience emitted with ID:', this.id);
    this.$emit('edit-experience', this.id);
  },
  confirmDelete() {
      // Emit an event to notify the parent component that delete is requested
      this.$emit('confirm-delete', this.id);
    },
},

};
</script>

<style scoped>
li {
  margin: 1rem 0;
  border: 1px solid #ccc;
  padding: 1rem;
}

h3,
p {
  font-size: 1rem;
  margin: 0.5rem 0;
}

.highlight {
  font-weight: bold;
}

.rating--poor {
  color: #b80056;
}

.rating--average {
  color: #330075;
}

.rating--great {
  color: #008327;
}
</style>