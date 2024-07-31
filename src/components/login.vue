<template>
    <div class="login-container">
      <h2>Login</h2>
      <form @submit.prevent="login">
        <div class="form-group">
          <label for="login">Login</label>
          <input type="text" id="login" v-model="loginData.login" required />
        </div>
        <div class="form-group">
          <label for="password">Senha</label>
          <input type="password" id="password" v-model="loginData.password" required />
        </div>
        <button type="submit">Entrar</button>
      </form>
      <p>Não tem uma conta? <a @click="register">Cadastre-se</a></p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        loginData: {
          login: '',
          password: ''
        }
      };
    },
    methods: {
      login() {
        // Lógica de login
        console.log('Login data:', this.loginData);
      },
      register() {
        // Lógica para redirecionar para a página de cadastro
        console.log('Redirect to registration page');
      }
    }
  };
  </script>
  
  <style scoped>
  .login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
  }
  
  button {
    width: 100%;
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  p {
    margin-top: 15px;
    text-align: center;
  }
  </style>
  