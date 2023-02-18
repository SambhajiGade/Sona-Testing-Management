<template>
  <!-- App.vue -->

  <v-app>
    <v-navigation-drawer app>
      <v-divider length="0">h</v-divider>

      <v-list dense nav>
        <img src="@/assets/sona.png" alt="">
 
        
        <v-divider></v-divider>

        <v-list-item  v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon >{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title style="text-align: left;font-weight: bold;">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    

    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-container fluid>
        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>
<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Home", icon: " mdi-home", to: "/HomeView" },
      { title: "Geometric Parameters ", icon: "mdi-dropbox", to: "/about" },
      { title: "FEA Data", icon: "mdi-calendar-clock", to: "/latestView" },
      {
        title: "FEA Contact Pattern",
        icon: "  mdi-account-box-outline",
        to: "/FEAContact",
      },
      { title: "Dashboard", icon: " mdi-home", to: "/Dashboard/ " },
    ],
  }),
};
</script>
