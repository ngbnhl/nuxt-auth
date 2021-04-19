<template>
  <div>
    <v-expansion-panels focusable>
      <v-expansion-panel>
        <v-expansion-panel-header>Sử dụng scheme laravelJWT</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-card>
            <v-card-text>
              <div class="text--primary">
                <pre> auth: {
    strategies: {
        'laravelJWT': {
                  provider: 'laravel/jwt',
                  url: '<'laravel url'>',
                  endpoints: {
                ...
                },
                  token: {
                   property: 'access_token',
                   maxAge: 60 * 60
                },
                  refreshToken: {
                    maxAge: 20160 * 60
                  },
                },
        }
    }
</pre>
              </div>
            </v-card-text>
            <v-card-actions>
              <v-btn
                color="teal accent-4"
                text
                @click="reveal = true"
              >
                Giải thích
              </v-btn>
            </v-card-actions>

            <v-expand-transition>
              <v-card
                v-if="reveal"
                class="transition-fast-in-fast-out v-card--reveal"
              >
                <v-card-text v-for="item in items" :key="item.title" class="pb-0">
                  <p class="font-weight-bold">
                    {{ item.title }}
                  </p>
                  <p>{{ item.text }} </p>
                </v-card-text>
                <v-card-actions class="pt-0">
                  <v-btn
                    color="teal accent-4"
                    text
                    @click="reveal = false"
                  >
                    Close
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-expand-transition>
          </v-card>
        </v-expansion-panel-content>
        <v-expansion-panel-content>
          <v-card>
            <v-img
              src="refresh.png"
            ></v-img>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <br>
    <v-expansion-panels focusable>
      <v-expansion-panel>
        <v-expansion-panel-header>Sử dụng Proxy</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-card>
            <v-card-text>
              <div class="text--primary">
                <pre>  axios: {
    proxy: true
  },
  proxy: {
    '/laravel': {
      target: 'https://laravel-auth.nuxtjs.app',
      pathRewrite: { '^/laravel': '/' }
    }
  },
</pre>
              </div>
            </v-card-text>
            <v-card-actions>
              <v-btn
                color="teal accent-4"
                text
                @click="reveal2 = true"
              >
                Giải thích
              </v-btn>
            </v-card-actions>

            <v-expand-transition>
              <v-card
                v-if="reveal2"
                class="transition-fast-in-fast-out v-card--reveal"
                style="height: 100%;"
              >
                <v-card-text v-for="item in proxy" :key="item.title" class="pb-0">
                  <p class="text--primary">
                    {{ item.title }}
                  </p>
                  <p>{{ item.text }} </p>
                </v-card-text>
                <v-card-actions class="pt-0">
                  <v-btn

                    color="teal accent-4"
                    text
                    @click="reveal2 = false"
                  >
                    Close
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-expand-transition>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <br>
    <v-expansion-panels focusable>
      <v-expansion-panel>
        <v-expansion-panel-header>Cài đặt loginWith</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-card>
            <v-card-text>
              <div class="text--primary">
                <pre>  this.$auth.loginWith('laravelJWT', {
  data: {
    email: '__email__',
    password: '__password__'
  }
})
                </pre>
              </div>
            </v-card-text>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <br>
    <v-expansion-panels focusable>
      <v-expansion-panel>
        <v-expansion-panel-header>Refresh Token</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-card>
            <v-card-text>
              <div class="text--primary">
                <p class="font-weight-light">
                  Laravel JWT không cung cấp 'refresh token'; token và refreshToken hết hạn như được xác định trong cấu
                  hình của Laravel JWT.<br>

                  Nhà cung cấp của chúng tôi sẽ quản lý việc làm mới tự động dựa trên tuổi thọ của token.<br>

                  Thời gian tồn tại của mã thông báo mặc định là 1 giờ và refreshToken là 2 tuần dựa trên cấu hình. Đảm
                  bảo rằng cấu hình JWT Laravel của bạn khớp với cấu hình Auth Nuxt Laravel JWT của chúng tôi.
                </p>
              </div>
            </v-card-text>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  name: "jwt",
  data: () => ({
    reveal: false,
    reveal2: false,
    items: [
      {id: 1, title: 'provider', text: 'Áp dụng provider laravelJWT cho việc xác thực'},
      {id: 2, title: 'url', text: 'Đường dẫn gọi tới API'},
      {id: 3, title: 'endpoints', text: 'endpoints API '},
      {id: 4, title: 'token', text: 'property sẽ lấy tên trường API trả về'},
      {id: 5, title: 'refreshToken', text: 'Không sử dụng'},

    ],
    proxy: [
      {id: 1, title: '/laravel', text: 'tên đường dẫn proxy'},
      {id: 2, title: 'target', text: 'đường dẫn gọi tới API'},
      {id: 3, title: 'pathRewrite', text: 'Sửa lại đường dẫn của Proxy'},
    ],
  }),
}
</script>

<style scoped>

.v-card--reveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}

</style>
