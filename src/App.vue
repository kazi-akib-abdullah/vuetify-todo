<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" mobile-breakpoint="768" app>
      <v-img
        class="pa-4 pt-7"
        src="mountains.jpg"
        height="170"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
      >
        <v-avatar size="70" class="mb-2"><img src="me.jpg" alt="Kazi Akib Abdullah"></v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">Kazi Akib Abdullah</div>
        <div class="white--text text-subtitle-2">akib_abdullah</div>
      </v-img>
      <!-- <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6"> Vuetify Todo </v-list-item-title>
          <v-list-item-subtitle> Best Todo Ever </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider> -->

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      src="mountains.jpg"
      prominent
      height="170"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="pa-0 header-container">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search></search>
        </v-row>
        <v-row>
          <v-app-bar-title class="ml-4 text-h4">{{ $store.state.appTitle}}</v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time></live-date-time>
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar></snackbar>
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from "@/components/Global/Snackbar.vue";
import Search from "./components/Tools/Search.vue";
import LiveDateTime from "./components/Tools/LiveDateTime.vue";

export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  components: {
    snackbar: Snackbar,
    search: Search,
    "live-date-time": LiveDateTime,
  },
};
</script>

<style lang="sass">
  .header-container
    max-width: none !important
</style>