<template>
  <v-card>
    <v-card-title>
      <span class="headline">Login Form</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
        >
          <v-row>
          <v-col cols="12">
            <v-text-field
              label="Email*"
              required
              outlined
              placeholder="Email"
              :rules="emailRules"
              v-model="email"
              clearable
              prepend-icon="mdi-email"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              label="Password*"
              type="password"
              required
              outlined
              clearable
              v-model="password"
              :rules="passwordRules"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
              :type="showPassword ? 'text' : 'password'"
            ></v-text-field>
          </v-col>
          </v-row>
        </v-form>
      </v-container>
      <small>*indicates required field</small>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        color="pink accent-1"
        text
        @click="login()"
        :disabled="!valid"
      >
        Login
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "UserLoginComponent",
  data: () => ({
    valid: true,
    showPassword: false,
    email: '',
    password: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    passwordRules: [
      v => !!v || 'E-mail is required']
  }),
  methods: {
    async login() {
      try{
        await this.$auth.loginWith("laravelSanctum", {
          data: {
            email: this.email,
            password: this.password
          }
        });
      }catch(err){
        console.error(err);
      }
    },
  }
}
</script>

<style scoped>

</style>
