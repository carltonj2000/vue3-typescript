<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>@ {{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import EventService from '@/services/EventService'
// eslint-disable-next-line no-unused-vars
import { EventItem } from '@/types'

export default defineComponent({
  name: 'EventDetails',
  props: {
    id: Number
  },
  data() {
    return {
      event: {} as EventItem
    }
  },
  async created() {
    try {
      const response = await EventService.getEvent(this.id || 123)
      this.event = response.data
    } catch (e) {
      console.log(e)
    }
  }
})
</script>
