<template>
  <div
    class="project"
    :class="{ complete: project.complete }"
  >
    <div class="actions">
      <h3
        @click="showDetails = !showDetails"
      >{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
          <span class="material-icons">edit</span>
        </router-link>
        <span
          @click="handleDeleteProject"
          class="material-icons"
        >delete</span>
        <span
          @click="toggleComplete"
          class="material-icons tick"
        >done</span>
      </div>
    </div>
    <div
      v-if="showDetails"
      class="details"
    >
      {{ project.details }}
    </div>
  </div>
</template>

<script>

export default {
  props: [
    'project',
  ],

  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id,
    }
  },

  methods: {
    handleDeleteProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.project.id))
        .catch(err => console.log(err.message))
    },

    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
      }).then(() => this.$emit('complete', this.project.id))
        .catch(err => console.log(err.message))
    },
  },
}
</script>

<style>
.project {
  margin: 20px auto;
  background: #fff;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  border-left: 4px solid #e90074;
  transition: .4s;
}

.project.complete {
  border-left: 4px solid #00ce89;
}

.project.complete .tick {
  border-radius: 50%;
  color: #fff;
  background: #00ce89;
}

h3 {
  cursor: pointer;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
  transition: .4s;
}

.material-icons:hover {
  color: #777;
}
</style>