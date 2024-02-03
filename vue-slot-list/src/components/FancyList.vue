<script setup lang="ts">
import { onBeforeMount, ref, type Ref } from "vue";
import DummyData from "@/assets/data.json";
import axios from "axios";
import { type Event } from "@/types/event-types";

const eventData: Ref<Event[] | undefined> = ref();

//mock remote data fetching

type Props = {
  activeIndex: Number | null;
};

const props = defineProps<Props>();

onBeforeMount(async () => {
  await getEvents();
});

const getEvents = async () => {
  try {
    const response = await axios.get(
      "https://app.ticketmaster.com/discovery/v2/events.json",
      {
        params: {
          classificationName: "rap",
          // sort: "date,name,asc",
          apikey: "pr5ET3AWxZ5FYoADVHGGriBKXkZyleS1",
          size: 50,
        },
      }
    );

    const events = response.data._embedded.events.map((event: any) => {
      return {
        eventId: event.id,
        name: event.name,
        date: event.dates.start.localDate,
        time: event.dates.start.localTime,
        venue: event?._embedded?.venues[0]?.name,
        url: event.url,
        ticketLimit: event.accessibility?.ticketLimit,
        image: event.images[0]?.url,
        country: event._embedded.venues[0]?.country.name,
        city: event._embedded.venues[0]?.city.name,
      };
    });
    if (events) {
      eventData.value = events;
      console.log(eventData.value);
      return;
    }
    console.log("No events found");
  } catch (error) {
    console.error(error);
  }
};
</script>

<template>
  <ul style="margin-top: 1rem" v-if="eventData">
    <li
      v-for="(event, index) in eventData"
      :key="event.id"
      :id="`item-${index}`"
      :class="{ active: activeIndex === index }"
    >
      <slot name="item" v-bind="event" :id="`item-${index}`" />
    </li>
  </ul>
  <div v-else>Loading...</div>
</template>

<style scoped>
ul {
  list-style-type: none;
}
ul li {
  padding: 5px 20px;
  margin: 10px;
  background: #fff;
  border: solid 1px #ddd;
}

.active {
  background: #41b883;
}
</style>
