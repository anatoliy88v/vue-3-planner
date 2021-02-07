<template>
  <div class="home">
    <FilterNav
      :filter="filter"
      @filterChange="filter = $event"
    />
    <div
      v-if="filteredProjects.length"
    >
      <div
        v-for="project in filteredProjects"
        :key="project.id"
      >
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject'
import FilterNav from '../components/FilterNav'

export default {
  name: 'Home',

  components: {
    SingleProject,
    FilterNav,
  },

  data() {
    return {
      projects: [],
      filter: 'all'
    }
  },

  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  },

  computed: {
    filteredProjects() {
      if (this.filter === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.filter === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  },

  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },

    handleComplete(id) {
      const updatedProject = this.projects.find((project) => {
        return project.id === id
      })

      updatedProject.complete = !updatedProject.complete
    },
  }
}
</script>
