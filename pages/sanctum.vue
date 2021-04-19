<template>
  <div>
    <a href="https://docs.google.com/spreadsheets/d/1VKNFw5ZGYgNSPPk4S6qgZQcgAcPEPhXx8PKNvDgSbwQ/edit#gid=0"
       target="_blank">Sanctum
      Research</a>
    <v-stepper v-model="e1">
      <v-stepper-header>
        <v-stepper-step
          :complete="e1 > 1"
          step="1"
        >
          nuxt.config.js
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step
          :complete="e1 > 2"
          step="2"
        >
          Proxy
        </v-stepper-step>

        <v-divider></v-divider>

        <v-stepper-step step="3">
          Login
        </v-stepper-step>
      </v-stepper-header>

      <v-stepper-items>
        <v-stepper-content step="1">
          <v-card
            class="mb-12"
          >
          <pre>auth: {
  strategies: {
    'laravelSanctum': {
       provider: 'laravel/sanctum',
       url: '<'laravel url'>'
       },
     }
  }
</pre>
          </v-card>

          <v-btn
            color="primary"
            @click="e1 = 2"
          >
            >
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="2">
          <v-card
            class="mb-12"
          >
          <pre>axios: {
    proxy: true,
    credentials: true
  },
proxy: {
    '/laravel': {
      target: 'https://laravel-auth.nuxtjs.app',
      pathRewrite: { '^/laravel': '/' }
    }
  },
          </pre>
          </v-card>
          <v-btn @click="e1-=1">
            <
          </v-btn>
          <v-btn
            color="primary"
            @click="e1 = 3"
          >
            >
          </v-btn>
        </v-stepper-content>

        <v-stepper-content step="3">
          <v-card
            class="mb-12"
          >
          <pre>this.$auth.loginWith('laravelSanctum', {
  data: {
    email: '',
    password: ''
  }
})
          </pre>
          </v-card>
          <v-btn @click="e1-=1">
            <
          </v-btn>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
    <v-row
      justify="center"
    >
      <v-btn
        class="ma-2"
        color="pink lighten-2"
        @click="expand = !expand"
      >
        Workflow
      </v-btn>

    </v-row>

    <v-expand-transition>
      <div class="d-flex justify-center">
        <v-img
          v-show="expand"
          max-height="700"
          max-width="700"
          src='sanctum.png'
        ></v-img>
      </div>
    </v-expand-transition>
  </div>
</template>

<script>
export default {
  name: "sanctum",
  data() {
    return {
      e1: 1,
      expand: false,
    }
  },
}
</script>

<style scoped>

</style>
