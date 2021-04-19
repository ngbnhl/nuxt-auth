<template>
  <div>
    <v-card>
      <v-toolbar
      >
        <v-toolbar-title>Cài đặt thư viện Auth</v-toolbar-title>
        <template v-slot:extension>
          <v-tabs
            v-model="tab"
            align-with-title
          >
            <v-tabs-slider color="pink"></v-tabs-slider>

            <v-tab
              v-for="item in items"
              :key="item"
            >
              {{ item }}
            </v-tab>
          </v-tabs>
        </template>
      </v-toolbar>

      <v-tabs-items v-model="tab">
        <v-tab-item
          v-for="item in items"
          :key="item"
        >
          <v-card v-if="item =='npm'" flat>
            <v-card-text>
              npm install --save-exact @nuxtjs/auth-next <br>
              npm install @nuxtjs/axios

            </v-card-text>
          </v-card>
          <v-card v-else flat>
            <v-card-text>
              yarn add --exact @nuxtjs/auth-next <br>
              yarn add @nuxtjs/axios
            </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
    <br>
    <v-card>
      <v-card-text>
        <p class="display-1 text--primary">
          Sử dụng module Auth
        </p>
        <p>nuxt.config.js</p>
        <div class="text--primary">
       <pre>{
           modules: [
             '@nuxtjs/axios',
             '@nuxtjs/auth-next'
           ],
             auth: {
             // Options
           }
}
</pre>
        </div>
      </v-card-text>
    </v-card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tab: null,
      items: [
        'npm', 'yarn'
      ],
    }
  },
}
</script>
