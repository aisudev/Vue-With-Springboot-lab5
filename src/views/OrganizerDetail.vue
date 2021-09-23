<template>
  <div v-if="organizer" class="container">
    <img :src="organizer.imageUrls" />
    <h2>@{{ organizer.name }}</h2>
    <EventOffCard
      v-for="event in organizer.ownEvents"
      :key="event.id"
      :event="event"
    />
  </div>
</template>

<script>
import { watchEffect } from '@vue/runtime-core'
import OrganizerService from '@/services/OrganizerService.js'
import EventOffCard from '@/components/EventOffCard.vue'

export default {
  name: 'OrganizerDetail',
  components: {
    EventOffCard
  },
  props: {
    organizerId: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      organizer: null
    }
  },
  created() {
    watchEffect(() => {
      OrganizerService.getOrganizer(this.organizerId)
        .then((result) => {
          this.organizer = result.data
        })
        .catch((err) => {
          console.log(err)
        })
    })
  }
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

img{
  width: 300px;
}
</style>
