<template>
  <div>
    <v-card>
      <v-card-title class="deep-orange lighten-3 white--text headline">
        <a
          href="https://docs.google.com/spreadsheets/d/1p8kmNc5oZ11hgLaaliJyfi6Wla3VtXPrgihhtATovto/edit#gid=128062138>"
        >Options Auth
        </a>
      </v-card-title>
      <v-row
        class="pa-4"
        justify="space-between"
      >
        <v-list>
          <v-list-item-group
            v-model="selectedItem"
            color="orange lighten-1"
          >
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
            >
              <v-list-item-icon>
                <v-icon v-text="item.icon"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title v-text="item.text"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>

        <v-divider vertical></v-divider>

        <v-col
          class="d-flex text-center"
        >
          <v-scroll-y-transition mode="out-in">
            <div
              v-if="!selected"
              class="title grey--text text--lighten-1 font-weight-light"
              style="align-self: center;"
            >
              Select an Option
            </div>
            <v-card
              v-else
              :key="selected.id"
              class="pt-6 mx-auto"
              flat
              max-width="400"
            >
              <v-card-text>
                <h3 class="headline mb-2 ">
                  {{ selected.text }}
                </h3>
                <div class="orange--text mb-2">
                  {{ selected.description }}
                </div>
              </v-card-text>
              <v-divider></v-divider>
              <v-row
                class="text-left"
                tag="v-card-text"
              >
                <v-col
                  class="text-right mr-4 mb-2"
                  cols="5"
                  tag="strong"
                >
                  Mặc định:
                </v-col>
                <v-col>{{ selected.default }}</v-col>
                <v-col
                  class="text-right mr-4 mb-2"
                  cols="5"
                  tag="strong"
                >
                  Ghi chú:
                </v-col>
                <v-col>
                  {{ selected.note }}
                </v-col>
                <v-col
                  class="text-right mr-4 mb-2"
                  cols="5"
                  tag="strong"
                >
                  Phone:
                </v-col>
                <!--              <v-col>{{ selected.phone }}</v-col>-->
              </v-row>
            </v-card>
          </v-scroll-y-transition>
        </v-col>
      </v-row>
    </v-card>
    <br>
    <v-expansion-panels>
      <v-expansion-panel>
        <v-expansion-panel-header>
          Tổng quan
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-card>
            <v-img
              src="options.png"
            ></v-img>
          </v-card>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  name: "options",
  data: () => ({
    selectedItem: '',
    items: [
      {
        text: 'redirect',
        icon: 'mdi-axis-arrow',
        id: 1,
        description: 'Điều hướng người dùng dựa trên các hành động',
        default:
          '  redirect: {\n' +
          '    login: \'/login\',\n' +
          '    logout: \'/\',\n' +
          '    callback: \'/login\',\n' +
          '    home: \'/\'\n' +
          '  }\n',
        note: 'Có thể vô hiệu hóa từng thành phần bằng cách cài đặt false cho thành phần đó, hoặc vô hiệu hóa tất cả thì cài đặt redirect: false'
      },
      {
        text: 'watchLoggedIn',
        icon: 'mdi-eye-circle',
        id: 2,
        description: 'Chuyển hướng người dùng dựa trên các hành động đăng nhập/đăng xuất',
        default: 'true',
        note: 'Khi được cài đặt false, người dùng sẽ không được chuyển trang sau khi đăng nhập/đăng xuất (login/logout ở trang nào thì giữ nguyên vị trí ở trang đó)'

      },
      {
        text: 'rewriteRedirects',
        icon: 'mdi-swap-horizontal',
        id: 3,
        description: 'Thay đổi điều hướng người dùng của thành phần redirect.home',
        default: 'true',
        note: 'Có 3 trường hợp sẽ giải thích rõ hơn bằng demo'
      },
      {
        text: 'fullPathRedirect',
        icon: 'mdi-database-arrow-right',
        id: 4,
        description: 'Sử dụng Query params điều hướng người dùng',
        default: 'false',
        note: 'Chưa sử dụng bao giờ'
      },
      {
        text: 'token',
        icon: 'mdi-compass-rose',
        id: 5,
        description: 'Quy định cách đặt tên biến token',
        default: 'prefix: _token.',
        note: 'option này chỉ dùng để đặt tên key cho việc lưu trữ, khác với option token trong các schemes sử dụng token'
      },
      {
        text: 'localStorage',
        icon: 'mdi-nas',
        id: 6,
        description: 'Sử dụng localStorage để lưu trữ token',
        default: 'true',
        note: 'Có thể vô hiệu hóa localStorage bằng cách cài đặt false. Token sẽ không được lưu vào localStorage nữa.'
      },
      {
        text: 'cookie',
        icon: 'mdi-cookie',
        id: 7,
        description: 'Sử dụng cookie để lưu trữ token',
        default: 'true',
        note: ' Việc sử dụng cookie là bắt buộc đối với các ứng dụng chế độ SSR vì xác thực khi tải trang đầu tiên chỉ xảy ra ở phía máy chủ và localStorage không khả dụng trên máy chủ.Vô hiệu hóa việc sử dụng cookieStorage bằng cách cài đặt false.'
      },
      {
        text: 'vuex.namespace',
        icon: 'mdi-vuejs',
        id: 8,
        description: 'Chỉ định namespace cho VueX để quản lý state user và loggedIn',
        default: 'auth',
        note: 'Trong trường hợp tạo thêm file có tên auth.js trong store, thì sẽ bị duplicate tên file [vuex] duplicate namespace auth/ for the namespaced module auth'
      },
      {
        text: 'resetOnError',
        icon: 'mdi-alert-circle',
        id: 9,
        description: 'reset lại Auth khi xảy ra lỗi ',
        default: 'false',
        note: 'Hiện tại cài đặt rồi nhưng không rõ là có chạy hay không'
      },
      {
        text: 'plugins',
        icon: 'mdi-toy-brick',
        id: 10,
        description: 'Cho phép các plugin ngoài sử dụng $auth',
        default: '',
        note: ''
      },
      {
        text: 'scopeKey',
        icon: 'mdi-telescope',
        id: 11,
        description: 'Kiểm tra quyền của đối tượng User',
        default: 'scope',
        note: ''
      },
    ],
  }),
  computed: {
    selected() {
      if (this.selectedItem === '') return undefined
      const id = this.selectedItem;
      return this.items[id];
    },
  },
}
</script>

<style scoped>

</style>
