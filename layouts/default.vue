<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="clipped"
      :mini-variant="miniVariant"
      app
      fixed
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          exact
          router
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      app
      fixed
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="fixed = !fixed"
      >
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title"/>
      <v-spacer/>

      <div v-if="isAuthenticated">
        <!--User Avatar Menu-->
        <v-menu
          bottom
          min-width="200px"
          offset-y
          rounded
        >
          <template v-slot:activator="{ on }">
            <v-btn
              v-on="on"
              icon
              x-large
            >
              <v-avatar>
                <img
                  alt="User"
                  src="https://cdn.vuetifyjs.com/images/john.jpg"
                >
              </v-avatar>
            </v-btn>
          </template>
          <user-avatar-menu></user-avatar-menu>
        </v-menu>
      </div>

      <div v-else>
        <!--Register Form-->
        <v-dialog width="unset">
          <template #activator="{ on: dialog }">
            <v-tooltip bottom>
              <template #activator="{ on: tooltip }">
                <v-btn
                  v-on="{ ...tooltip, ...dialog }"
                  icon
                >
                  <v-icon>mdi-account-plus</v-icon>
                </v-btn>
              </template>
              <span>Register</span>
            </v-tooltip>
          </template>
          <user-register-component/>
        </v-dialog>

        <!--Login Form-->

        <v-tooltip bottom>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              v-bind="attrs"
              v-on="on"
              icon
              nuxt to="/login"
            >
              <v-icon>mdi-login-variant</v-icon>
            </v-btn>
          </template>
          <span>Login</span>
        </v-tooltip>
      </div>
      <!--Theme Color-->
      <v-btn
        icon
        @click="changeTheme()"
      >
        <v-icon>mdi-theme-light-dark</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt/>
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import UserRegisterComponent from "../components/UserRegisterComponent";
import UserLoginComponent from "../components/UserLoginComponent";
import {mapGetters} from 'vuex';
import UserAvatarMenu from "../components/UserAvatarMenu";

export default {
  computed: {
    ...mapGetters(['isAuthenticated', 'loggedInUser'])
  },
  components: {UserAvatarMenu, UserLoginComponent, UserRegisterComponent},
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Setup',
          to: '/inspire'
        },
        {
          icon: 'mdi-asterisk',
          title: 'JWT',
          to: '/jwt'
        },
        {
          icon: 'mdi-atom',
          title: 'Sanctum',
          to: '/sanctum'
        },
        {
          icon: 'mdi-cat',
          title: 'Options',
          to: '/options'
        },
        {
          icon: 'mdi-bug',
          title: 'Bug & Error',
          to: '/bug'
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Nuxt Auth',

    }
  },
  methods: {
    changeTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
  }
}
</script>
