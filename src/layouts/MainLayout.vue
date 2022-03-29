<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>

        <q-toolbar-title class="row items-center q-gutter-md">
          <div class="col-shrink"><img
              alt="FindAHikingBuddy Logo"
              src="~assets/logo-100x100.png"
              style="width: 50px; height: 50px"
            /></div>
          <div class="col">Find a Hiking Buddy</div>
        </q-toolbar-title>

        <div class="row q-gutter-sm">
          <div>
            <q-btn color="secondary">Sign Up</q-btn>
          </div>
          <q-btn color="secondary">Sign In</q-btn>
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
