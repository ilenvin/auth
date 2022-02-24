<template>
     <v-app-bar
      app
      color="indigo lighten-1"
      dark
    >
      <div class="d-flex align-center">
        <router-link to="/">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />
        </router-link>

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <router-link to="/login">
      <Button btnText="Log in" ></Button>
      </router-link>
      
      <router-link to="/signup">
      <Button btnText="Sign up"></Button>
      </router-link>
      <!-- :hideBtn="false" -->
    </v-app-bar>
</template>

<script>
/* eslint-disable */
import Button from './Button.vue'
export default {
  components: { Button },
  name: 'NavBar',
  data: () => ({
  })
}
</script>
