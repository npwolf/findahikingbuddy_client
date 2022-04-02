<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="bg-white justify-between">
        <div class="row q-gutter-sm">
          <div>
            <q-btn color="red">Schedule a Hike</q-btn>
          </div>
        </div>
        <div>
          <!-- <q-toolbar-title class="row items-center q-pa-xs q-gutter-md"> -->
          <!-- <div class="col-shrink q-pa-xs"><img
              alt="FindAHikingBuddy Logo"
              src="~assets/logo4.png"
              style="width: 226px; height: 130px"
            /></div> -->
          <div
            class="col title"
            style="color:black"
          >Find a Hiking Buddy</div>
          <!-- </q-toolbar-title> -->
        </div>
        <div class="row q-gutter-sm">
          <q-btn color="secondary">Login or Signup</q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "MainLayout",

  components: {
  },

  setup () {
    const leftDrawerOpen = ref(false);

    return {
    };
  },
});
</script>

<style scoped>
.title {
  font-family: "Oswald", sans-serif;
  font-size: 35px;
}
</style>
