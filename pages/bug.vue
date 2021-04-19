<template>
  <v-row justify="center">
    <v-expansion-panels inset>
      <v-expansion-panel v-for="bug in bugs" :key="bug.id">
        <v-expansion-panel-header>{{ bug.name }}</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-img
          :src="`${bug.img}`"></v-img>
          <br>
          <v-divider></v-divider>
          <p class="font-weight-light">{{bug.solve}}</p>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </v-row>
</template>
<script>
export default {
  name: "bug",
  data: ()=>({
  bugs: [
    {
      id:1,
      name:'Cookie has been rejected for invalid domain',
      solve:'Xem lại cấu hình domain phía API',
      img:'invaliddomain.png',
    },
    {
      id:2,
      name:'Cookie has been rejected because it is already expired',
      solve:'Điều tra việc xóa các cookie hết hạn ra khỏi brower hoặc do API trả cookie hết hạn',
      img:'expiredcookie.png',
    },
    {
      id:3,
      name:'Cookie has been rejected because there is already an HTTP-Only cookie but script tried to store a new one',
      solve:'Bật chế độ HTTP-Only rồi thì script không đọc được nữa',
      img:'httpOnly.png',
    },
    {
      id:4,
      name:'HTTP 401 Unauthorized khi sử dụng Proxy',
      solve:'Kiểm tra lại TARGET của proxy',
      img:'',
    },
    {
      id:5,
      name:'HTTP 419 Unknown Status khi gọi Axios',
      solve:'Kiểm tra lại withCredentials của axios khi gọi API',
      img:'',
    },
    {
      id:6,
      name:'HTTP 422 Unprocessable Entity khi gọi Axios',
      solve:'Kiểm tra lại data khi gửi xuống API, có thể có một(vài) data đã tồn tại trong API',
      img:'',
    },
  ]
  }),
}
</script>

<style scoped>

</style>
