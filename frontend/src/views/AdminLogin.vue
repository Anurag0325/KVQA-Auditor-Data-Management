<template>
    <v-app>
    <v-container>
    <v-app-bar app color="black" dark>
        <v-toolbar-title>Admin Dashboard</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn color="error" @click="userlogin">User Login</v-btn>
      </v-app-bar>
    </v-container>
    <v-container>
      <v-card class="pa-5 mx-auto" max-width="400">
        <v-card-title class="text-center">Admin Login</v-card-title>
        <v-card-text>
          <v-form @submit.prevent="adminLogin">
            <v-text-field label="Email" v-model="email" required></v-text-field>
            <v-text-field label="Password" v-model="password" type="password" required></v-text-field>
            <v-btn type="submit" color="primary" block>Login</v-btn>
          </v-form>
          <p v-if="errorMessage" class="red--text">{{ errorMessage }}</p>
        </v-card-text>
      </v-card>
    </v-container>
    </v-app>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    data() {
      return {
        email: "",
        password: "",
        errorMessage: ""
      };
    },
    methods: {
        async adminLogin() {
  try {
    // const response = await axios.post("http://127.0.0.1:5000/admin/login", {
    const response = await axios.post("https://kvqa-auditor-data-management.onrender.com//admin/login", {
      email: this.email,
      password: this.password
    });

    // ✅ `is_admin` will always be True if login is successful
    localStorage.setItem("token", response.data.token);
    this.$router.push("/admin/dashboard"); // Redirect to Admin Dashboard
  } catch (error) {
    this.errorMessage = error.response?.data?.error || "Login failed";
  }
},

      userlogin() {
        this.$router.push('/')
      }
    }
  };
  </script>
  
  <style scoped>
  @import 'vuetify/styles';
  </style>
  