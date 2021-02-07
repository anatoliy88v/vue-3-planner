<template>
  <div class="filter-nav">
    <button
      :class="{ active: filter === 'all' }"
      @click="handleFilter('all')"
    >View All</button>
    <button
      :class="{ active: filter === 'completed' }"
      @click="handleFilter('completed')"
    >Completed</button>
    <button
      :class="{ active: filter === 'ongoing' }"
      @click="handleFilter('ongoing')"
    >Ongoing</button>
  </div>
</template>

<script>
export default {
  props: [
    'filter'
  ],

  methods: {
    handleFilter(by) {
      this.$emit('filterChange', by)
    }
  }
}
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
  transition: .4s;
}
.filter-nav button.active {
  color: #555;
}
</style>