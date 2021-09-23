<template>
  <div class="container" @click="goTo">
    <h2>@{{ organizer.name }}</h2>
  </div>
</template>

<script>
export default {
  name: 'OrganizerCard',
  props: {
    organizer: {
      type: Object,
      required: true
    }
  },
  methods: {
    goTo() {
      this.$router.push({
        name: 'OrganizerDetail',
        params: { organizerId: this.organizer.id }
      })
    }
  }
}
</script>

<style scoped>
.container {
  width: 300px;
  border: 1px solid gray;
  margin: 5px;
}

.container:hover {
  box-shadow: 0 0 1px 2px black;
  cursor: pointer;
}
</style>
