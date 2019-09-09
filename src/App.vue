<template>
  <div id="app">
    <login-page v-if=" view === 'login' "
      @showRegisterPage = "showRegisterPage"
      @showDashboardPage = "showDashboardPage"
    />
    <register-page v-if=" view === 'register' "
      @backToLogin = "showLoginPage"
      @showLoginPage = "showLoginPage"
    />
    <dashboard-page v-if=" view === 'dashboard' "
    />
  </div>
</template>

<script>
import LoginPage from './components/Login';
import RegisterPage from './components/Register';
import DashboardPage from './components/dashboard'
import { Validator } from 'vee-validate';

export default {
  name: 'app',
  components: {
    LoginPage,
    RegisterPage,
    DashboardPage
  },
  data(){
    return {
      view: "login",
    }
  },

  mounted(){
    const dict = {
      custom: {
        email: {
          required: 'El email es requerido',
          email: ' debe escribir un email válido '
        },
        name: {
          required: () => 'Your name is empty'
        },
      }
    };

    Validator.localize('en', dict);
    // or use the instance method
  },

  methods: {
    showRegisterPage(){
      this.view = "register";
    },
    showLoginPage(){
      this.view = "login";
    },
    showDashboardPage(){
      this.view = "dashboard";
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
