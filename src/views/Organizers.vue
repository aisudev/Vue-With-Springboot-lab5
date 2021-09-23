<template>
  <div class="container">
    <OrganizerCard
      v-for="organizer in organizers"
      :key="organizer.id"
      :organizer="organizer"
    />
  </div>
</template>

<script>
import OrganizerCard from '@/components/OrganizerCard'
import { watchEffect } from '@vue/runtime-core'
import OrganizerService from '@/services/OrganizerService.js'
export default {
  name: 'Organizers',
  components: {
    OrganizerCard
  },
  data() {
    return {
      organizers: [
        {
          name: '1'
        }
      ]
    }
  },
  created() {
    watchEffect(() => {
      OrganizerService.getOrganizers()
        .then((result) => {
          this.organizers = result.data
          console.log(result)
        })
        .catch(() => {})
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
</style>
