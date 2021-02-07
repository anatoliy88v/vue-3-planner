<template>
  <form
    @submit.prevent="handleSubmit"
    class="add-project"
  >
    <label>Title:</label>
    <input
      v-model="title"
      type="text"
      required
    >
    <label>Details:</label>
    <textarea
      v-model="details"
      required
    ></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>

export default {
  data() {
    return {
      title: '',
      details: '',
    }
  },

  methods: {
    handleSubmit() {
      const project = {
        title: this.title,
        details: this.details,
        complete: false
      }

      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(project)
      }).then(() => {
        this.$router.push('/')
      }).catch(err => {
        console.log(err.message)
      })
    }
  },
}
</script>

<style>
.add-project {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
}

.add-project label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px;
}

.add-project input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}

.add-project textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}

.add-project button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: #fff;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}
</style>