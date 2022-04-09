<template>
  <q-page class="row items-start justify-center">
    <div class="row"></div>
    <div class="col-shrink">&nbsp;</div>
    <div class="q-pa-md col" style="max-width: 800px">
      <div class="row items-start justify-center">
        <div class="text-h4 q-pa-sm">Schedule a Hike</div>
      </div>
      <q-form class="q-gutter-y-md q-pa-sm">
        <q-card v-show="shouldShowHikeDetails">
          <q-card-section>
            <div class="text-h6">Hike Details</div>
          </q-card-section>
          <q-separator inset />
          <q-card-section>
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
            </div>

            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-grow">
                <q-input
                  filled
                  v-model="hikeUrl"
                  label="Link to Hike"
                  placeholder="https://www.alltrails.com/trail/..."
                />
              </div>
            </div>

            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-grow">&nbsp;</div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(2)"
                  >Next</q-btn
                >
              </div>
            </div>
          </q-card-section>
        </q-card>

        <q-card v-show="shouldShowMeetDetails">
          <q-card-section>
            <div class="text-h6">Meet When and Where</div>
          </q-card-section>
          <q-separator inset />
          <q-card-section>
            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-12 col-sm-3">
                <q-input
                  filled
                  v-model="meetDate"
                  mask="date"
                  label="Meet Date"
                  :rules="['date']"
                >
                  <template v-slot:append>
                    <q-icon name="event" class="cursor-pointer">
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
                <div id="geocoderCtrl" class="geocoder"></div>
              </div>
            </div>

            <div class="row q-gutter-y-md q-col-gutter-md">
              <!-- Map Display here -->
              <div class="map-holder col-grow">
                <div id="map"></div>
              </div>
            </div>
            <div class="row">
              <div class="col-grow">
                <span class="label"
                  >Meet Coordinates Latitude: {{ center[0] }} Longitude:
                  {{ center[1] }}</span
                >
              </div>
            </div>
            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-grow">&nbsp;</div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(1)"
                  >Back</q-btn
                >
              </div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(3)"
                  >Next</q-btn
                >
              </div>
            </div>
          </q-card-section>
        </q-card>

        <q-card v-show="shouldShowOtherDetails">
          <q-card-section>
            <div class="text-h6">Other</div>
          </q-card-section>
          <q-separator inset />
          <q-card-section>
            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="row max-width">
                <q-input
                  filled
                  type="textarea"
                  v-model="notes"
                  label="Other Details"
                  placeholder="This is an easy hike and anyone is welcome to join!"
                  class="max-width"
                />
              </div>
            </div>

            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-grow">&nbsp;</div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(2)"
                  >Back</q-btn
                >
              </div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(4)"
                  >Next</q-btn
                >
              </div>
            </div>
          </q-card-section>
        </q-card>

        <q-card v-show="shouldShowConfirmDetails">
          <q-card-section>
            <div class="text-h6">Confirm Event Details</div>
          </q-card-section>
          <q-separator inset />
          <q-card-section>
            <div class="row">
              <div class="row max-width">
                <div class="col-grow">Name of hike: {{ name }}</div>
              </div>
              <div class="row max-width">
                <div class="col-grow">Distance: {{ distance }} miles</div>
              </div>
              <div class="row max-width">
                <div class="col-grow">Gain: {{ gain }} feet</div>
              </div>
              <div class="row max-width">
                <div v-show="hikeUrl" class="col-grow">URL: {{ hikeUrl }}</div>
              </div>
              <div class="row max-width">
                <div class="col-grow">When: {{ largeMeetDate }}</div>
              </div>
              <div class="row max-width">
                <div class="col-grow">
                  Where: {{ center[0] }}, {{ center[1] }}
                </div>
              </div>
              <div class="row max-width">
                <div class="col-grow">Other: {{ note }}</div>
              </div>
            </div>

            <div class="row q-gutter-y-md q-col-gutter-md">
              <div class="col-grow">&nbsp;</div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="showPage(3)"
                  >Back</q-btn
                >
              </div>
              <div class="col-shrink">
                <q-btn color="secondary" @click.prevent="createEvent"
                  >Create</q-btn
                >
              </div>
            </div>
          </q-card-section>
        </q-card>
      </q-form>

      <!-- Coordinates Display here -->
      <!-- <div class="dislpay-arena">
        <div class="coordinates-header"></div>
        <div class="coordinates-header">
          <h3>Current Location</h3>
          <div class="form-group">
            <input
              type="text"
              class="location-control"
              :value="location"
              readonly
            />
            <button type="button" class="copy-btn" @click="copyLocation">
              Copy
            </button>
          </div>
          <button
            type="button"
            :disabled="loading"
            :class="{ disabled: loading }"
            class="location-btn"
            @click="getLocation"
          >
            Get Location
          </button>
        </div>
      </div> -->
    </div>

    <div class="col-shrink">&nbsp;</div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import moment from "moment";
import axios from "axios";
import mapboxgl from "mapbox-gl";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";
import "@mapbox/mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";

export default defineComponent({
  name: "PageCreate",
  methods: {
    createEvent() {
      console.log(this.meetTime);
    },
    async createMap() {
      try {
        mapboxgl.accessToken = this.access_token;
        this.map = new mapboxgl.Map({
          container: "map",
          style: "mapbox://styles/mapbox/outdoors-v11",
          center: this.center,
          zoom: 11,
        });

        let geocoder = new MapboxGeocoder({
          accessToken: this.access_token,
          mapboxgl: mapboxgl,
          marker: false,
        });

        //geocoder.addTo(geocoderCtrl)
        //this.map.addControl(geocoderCtrl);
        this.map.addControl(geocoder);
        geocoder.on("result", (e) => {
          const marker = new mapboxgl.Marker({
            draggable: true,
            color: "#D80739",
          })
            .setLngLat(e.result.center)
            .addTo(this.map);
          this.center = e.result.center;
          marker.on("dragend", (e) => {
            this.center = Object.values(e.target.getLngLat());
          });
          this.getLocation();
        });
      } catch (err) {
        console.log("map error", err);
      }
      // Do this here, otherwise map
      // is incorrect size.
      this.shouldShowMeetDetails = false;
    },
    async getLocation() {
      try {
        this.loading = true;
        const response = await axios.get(
          `https://api.mapbox.com/geocoding/v5/mapbox.places/${this.center[0]},${this.center[1]}.json?access_token=${this.access_token}`
        );
        this.loading = false;
        this.location = response.data.features[0].place_name;
      } catch (err) {
        this.loading = false;
        console.log(err);
      }
    },

    showPage(pageNumber) {
      this.shouldShowHikeDetails = false;
      this.shouldShowMeetDetails = false;
      this.shouldShowOtherDetails = false;
      this.shouldShowConfirmDetails = false;
      switch (pageNumber) {
        case 1:
          this.shouldShowHikeDetails = true;
          break;
        case 2:
          this.shouldShowMeetDetails = true;
          break;
        case 3:
          this.shouldShowOtherDetails = true;
          break;
        case 4:
          this.shouldShowConfirmDetails = true;
          break;
      }
    },
  },
  data() {
    return {
      name: "",
      distance: "",
      gain: "",
      meetDate: moment().add(3, "days").format("YYYY/MM/DD"),
      meetTime: "09:00",
      loading: false,
      location: "",
      access_token: process.env.VUE_APP_MAP_ACCESS_TOKEN,
      //center: [-119.5419754, 37.7459184],
      center: [0, 0],
      map: undefined,
      shouldShowHikeDetails: true,
      shouldShowMeetDetails: true,
      shouldShowOtherDetails: false,
      shouldShowConfirmDetails: false,
    };
  },
  mounted() {
    this.createMap();
  },
  computed: {
    largeMeetDate() {
      let meetDateTime = this.meetDate + " " + this.meetTime;
      return (
        moment(meetDateTime).format("ddd MMM Do YYYY h:mm a") +
        " - " +
        moment(meetDateTime).fromNow()
      );
    },
    fullMeetDetails() {
      return (
        this.largeMeetDate +
        " at " +
        this.location +
        " (" +
        this.center[0] +
        ", " +
        this.center[1] +
        ")"
      );
    },
  },
});
</script>

<style scoped>
#map {
  width: 100%;
  height: 300px;
}

.mapboxgl-ctrl-geocoder {
  min-width: 100%;
}

.max-width {
  width: 100%;
  max-width: 100%;
}
</style>
