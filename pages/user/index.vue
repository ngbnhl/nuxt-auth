<template>
  <v-card
    class="mx-auto"
    height="400"
    tile
  >
    <v-img
      height="100%"
      src="https://cdn.vuetifyjs.com/images/cards/server-room.jpg"
    >
      <v-row
        align="end"
        class="fill-height"
      >
        <v-col
          align-self="start"
          cols="12"
        >
          <v-row
            justify="center"
          >
            <v-avatar
              class="profile"
              size="164"
            >
              <v-img src="https://cdn.vuetifyjs.com/images/profiles/marcus.jpg"></v-img>
            </v-avatar>
          </v-row>
        </v-col>
        <v-col class="py-0">
          <v-list-item
            color="rgba(0, 0, 0, .4)"
            dark
          >
            <v-list-item-content>
              <v-list-item-title class="title">
                {{ loggedInUser.name }}
              </v-list-item-title>
              <v-list-item-subtitle>Network Engineer</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-col>
      </v-row>
    </v-img>
  </v-card>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
  name: "index",
  computed: {
    ...mapGetters(['loggedInUser'])
  }
}
</script>

<style scoped>

</style>
