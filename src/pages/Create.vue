<template>
  <q-page class="row items-start justify-center">
    <div class="col-shrink">&nbsp;</div>
    <div
      class="q-pa-md col"
      style="max-width: 800px"
    >
      <div>
        <q-form class="q-gutter-y-md">
          <q-input
            filled
            v-model="name"
            label="Name of Hike"
            placeholder="Xyz Trail"
          />
          <q-input
            filled
            v-model="distance"
            label="Distance in Miles"
            placeholder="5.5"
          />
          <q-input
            filled
            v-model="gain"
            label="Gain in Feet"
            placeholder="550"
          />
          <q-input
            filled
            v-model="meetDate"
            mask="date"
            label="Meet Date"
            :hint="largeMeetDate"
            :rules="['date']"
            style="max-width: 150px"
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

          <q-input
            v-model="meetTime"
            filled
            type="time"
            label="Meet Time"
            style="max-width: 150px"
          />

          <q-btn
            color="secondary"
            @click.prevent="createEvent"
          >Create</q-btn>
        </q-form>
      </div>
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
      return moment(this.meetDate).format("dddd, MMMM Do YYYY") + " - " + moment(this.meetDate).fromNow();
    },
  },
});
</script>

<style scoped>
</style>
