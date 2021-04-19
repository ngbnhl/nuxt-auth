<template>
  <v-card>
    <v-card-title>
      <span class="headline">User Registration</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="Legal first name*"
              required
              v-model="firstName"
              :rules="nameRules"
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="Legal middle name"
              hint="Middle name"
              v-model="middleName"
              :rules="nameRules"
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            sm="6"
            md="4"
          >
            <v-text-field
              label="Legal last name*"
              hint="Last name"
              persistent-hint
              required
              v-model="lastName"
              :rules="nameRules"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              label="Email*"
              required
              v-model="email"
              :rules="emailRules"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              label="Password*"
              type="password"
              required
              v-model="password"
              :rules="passwordRules"
            ></v-text-field>
          </v-col>
        </v-row>
      </v-container>
      <small>*indicates required field</small>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn
        color="blue darken-1"
        text
        @click="register()"
      >
        Register
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "UserRegisterComponent",
  data: () => ({
      firstName:'',
      middleName:'',
      lastName:'',
      email:'',
      password:'',
      nameRules: [
        v => !!v || 'Name is required'
      ],
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      passwordRules: [
        v => !!v || 'E-mail is required',
        v => (v && v.length >=8) || 'Password must be at least 8 characters',
      ],

    }),
  methods:{
    async register(){
      try {
        this.$axios.defaults.withCredentials = true;
       await this.$axios.get('http://localhost:8000/sanctum/csrf-cookie').then(response => {
           this.$axios.post('http://localhost:8000/api/register', {
            name: this.firstName+' '+this.middleName+ ' '+this.lastName,
            email: this.email,
            password: this.password
          })
        });
        await this.$auth.loginWith('laravelSanctum', {
          data: {
            email: this.email,
            password: this.password
          },
        })
      } catch (e) {
       console.error(e);
      }
    },
  }
}
</script>

<style scoped>

</style>
