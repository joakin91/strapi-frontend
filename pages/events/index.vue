<template>  
  <div>
      <form class="uk-search uk-search-large uk-align-center uk-margin">
          <span uk-search-icon></span>
          <input class="uk-search-input" v-model="query" type="search" placeholder="Search...">
      </form>

      <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@m uk-margin" v-for="event in filteredList" v-bind:key="event" uk-grid>
          <div class="uk-card-media-left uk-cover-container">
          </div>
          <div>
              <div class="uk-card-body">
                  <h3 class="uk-card-title">{{ event.name }}</h3>
                  <router-link :to="{ name: 'events-id', params: { id: event.id }}" tag="a" class="uk-button uk-button-primary">See event
                  </router-link>
              </div>
          </div>
      </div>

      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <p>No events found</p>
     </div>

  </div>

</template>

<script>  
// Import the events query
import eventsQuery from '~/apollo/queries/event/events'

export default {  
  data() {
    return {
      // Initialize an empty events variable
      events: [],
      query: ''
    }
  },
  apollo: {
    events: {
      prefetch: true,
      query: eventsQuery
    }
  },
  computed: {
    // Search system
    filteredList() {
      return this.events.filter(event => {
        return event.name.toLowerCase().includes(this.query.toLowerCase())
      })
    },
  }
}
</script> 