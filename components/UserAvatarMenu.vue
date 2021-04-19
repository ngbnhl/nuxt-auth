<template>
  <v-card>
    <v-list-item-content class="justify-center">
      <div class="mx-auto text-center">
        <h3> {{ loggedInUser.name }}</h3>
        <p class="caption mt-1">
          {{ loggedInUser.email }}
        </p>
        <v-divider class="my-3"></v-divider>
        <v-btn
          depressed
          nuxt
          rounded
          text
          to="/user"
        >
          My Profile
        </v-btn>
        <v-divider class="my-3"></v-divider>
        <v-btn
          depressed
          nuxt
          rounded
          text
          to="/user/edit"
        >
          Edit Account
        </v-btn>
        <v-divider class="my-3"></v-divider>
        <v-btn
          depressed
          rounded
          text
          @click="logout"
        >
          Disconnect
        </v-btn>
      </div>
    </v-list-item-content>
  </v-card>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
  name: "UserAvatarMenu",
  computed: {
    ...mapGetters(['loggedInUser'])
  },
  methods: {
    logout() {
      this.$auth.logout();
    },
  }
}
</script>

<style scoped>

</style>
