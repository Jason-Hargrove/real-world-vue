<template>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '@/types'
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService'

export default defineComponent({
  name: 'EventList',
  components: {
    EventCard,
  },
  data() {
    return {
      events: [] as EventItem[],
    }
  },
  created() {
    EventService.getEvents()
      .then((response) => {
        this.events = response.data
      })
      .catch((error) => {
        console.log(error)
      })
  },
})
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
