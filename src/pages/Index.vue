<template>
  <q-page class=" items-start justify-center">
    <q-img
      src="~assets/banner-people2.jpg"
      class="row banner-image"
    />
    <div class="row justify-center items-center search-bar">
      <div class="col-1">&nbsp;</div>
      <div class="col-grow">
        <q-input
          class="search shadow-4"
          outlined
          v-model="text"
          bg-color="white"
          label="Search by City"
        > <template v-slot:prepend>
            <q-icon name="place" />
          </template></q-input>
      </div>
      <div class="col-2">
        <q-select
          outlined
          bg-color="white"
          label="Distance"
          class="shadow-4"
        />
      </div>
      <div class="col-shrink">
        <q-btn color="secondary shadow-4">Search</q-btn>
      </div>
      <div class="col-1">&nbsp;</div>
    </div>

    <!-- <div class="row">
      <div class="col">
        <q-input
          class="search-box"
          rounded
          outlined
          v-model="text"
          label="Search by City"
        />
      </div>
    </div> -->

  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageIndex",
});
</script>

<style scoped>
.search-box {
  /* max-width: 900px; */
}

/* .search-bar-row {
  margin-top: -30px;
} */

/* div {
  border: 1px solid black;
} */

/* .bg-image {
  background-image: url(~assets/banner-people2.jpg);
  background-repeat: no-repeat;
  background-size: auto;
} */

/* .banner-image {
  max-height: 100px;
} */
</style>
