<template>  
<div>
  <client-only placeholder="Event registry">

    <div uk-grid>
        <div class="uk-width-1-3@m">

          <div class="uk-card uk-card-default uk-card-body uk-width-1-1@m">

            <form @submit.stop.prevent="handleSubmit">
                <fieldset class="uk-fieldset">

                    <legend class="uk-legend">Register event</legend>

                    <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Name</label>
                        <input class="uk-input" v-model="name" type="text" placeholder="Event name">
                    </div>

                    <div class="uk-margin">
                        <label class="uk-form-label" for="form-stacked-text">Date of event</label>
                        <datetime type="datetime" v-model="dateOfEvent"></datetime>
                    </div>

                    <button type="submit" class="uk-button uk-button-secondary uk-width-1-1">Submit</button>


                </fieldset>
            </form>
          </div>

        </div>
    </div>
  </client-only>

</div>  
</template>

<script>
import strapi from '~/utils/Strapi'
import { Datetime } from 'vue-datetime'
import 'vue-datetime/dist/vue-datetime.css'

export default {
  components: {
    datetime: Datetime
  },
  data() {
    return {
      name: '',
      dateOfEvent: '',
      complete: false,
      loading: false
    }
  },
  methods: {
    async handleSubmit() {
      this.loading = true
      let dateObject = new Date(this.dateOfEvent)
      try {
        await strapi.createEntry('events', {
          name: this.name,
          DateOfEvent: dateObject.getTime()
        })
        alert('Your event have been successfully submitted.')
        this.$router.push('/events')
      } catch (err) {
        console.log(err);
        this.loading = false
        alert('An error occurred.')
      }
    }
  }
}
</script> 