<template>
  <q-page class="row items-start justify-center">
    <div class="col-shrink">&nbsp;</div>
    <div
      class="q-pa-md col"
      style="max-width: 800px"
    >
      <q-form class="q-gutter-y-md">

        <div class="row">
          <div class="col-grow">
            <q-input
              filled
              v-model="name"
              label="Name of Hike"
              placeholder="Xyz Trail"
            />
          </div>
        </div>

        <div class="row q-gutter-y-md q-col-gutter-md">
          <!-- <div class="row q-gutter-y-md q-col-gutter-md"> -->
          <div class="col-12 col-sm-3">
            <q-input
              filled
              v-model="distance"
              label="Distance in Miles"
              placeholder="5.5"
            />
          </div>
          <div class="col-12 col-sm-3">
            <q-input
              filled
              v-model="gain"
              label="Gain in Feet"
              placeholder="550"
            />
          </div>
          <div class="col-12 col-sm-3">
            <q-input
              filled
              v-model="meetDate"
              mask="date"
              label="Meet Date"
              :hint="largeMeetDate"
              :rules="['date']"
            >
              <template v-slot:append>
                <q-icon
                  name="event"
                  class="cursor-pointer"
                >
                  <q-popup-proxy
                    ref="qDateProxy"
                    cover
                    transition-show="scale"
                    transition-hide="scale"
                  >
                    <q-date v-model="meetDate">
                      <div class="row items-center justify-end">
                        <q-btn
                          v-close-popup
                          label="Close"
                          color="primary"
                          flat
                        />
                      </div>
                    </q-date>
                  </q-popup-proxy>
                </q-icon>
              </template>
            </q-input>
          </div>
          <div class="col-12 col-sm-3">
            <q-input
              v-model="meetTime"
              filled
              type="time"
              label="Meet Time"
            />
          </div>
        </div>

        <div class="row">
          <div class="col-grow">
            <q-input
              filled
              v-model="name"
              label="Link to Hike"
              placeholder="https://www.alltrails.com/trail/..."
            />
          </div>
        </div>

        <div class="row justify-end">
          <q-btn
            color="secondary"
            @click.prevent="createEvent"
          >Create</q-btn>
        </div>
      </q-form>
    </div>

    <div class="col-shrink">&nbsp;</div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import moment from 'moment';

export default defineComponent({
  name: "PageCreate",
  methods: {
    createEvent () {
      console.log(this.meetTime);
    }
  },
  data () {
    return {
      name: "",
      distance: "",
      gain: "",
      meetDate: moment().add(3, "days").format('YYYY/MM/DD'),
      meetTime: "09:00"
    };
  },
  mounted () {

  },
  computed: {
    largeMeetDate () {
      return moment(this.meetDate).format("ddd MMM Do YYYY") + " - " + moment(this.meetDate).fromNow();
    },
  },
});
</script>

<style scoped>
</style>
