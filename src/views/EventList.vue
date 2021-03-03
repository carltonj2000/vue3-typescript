<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'

export default defineComponent({
  name: 'EventList',
  components: {
    EventCard
  },
  data() {
    return {
      events: null
    }
  },
  async created() {
    try {
      const response = await EventService.getEvents()
      this.events = response.data
    } catch (e) {
      console.log(e)
    }
  }
})
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
