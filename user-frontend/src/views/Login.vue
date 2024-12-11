<template>
  <div class="container">
    <div class="img-logo">
      <img src="../assets/images/Logo-BibliNovaEra-removebg-preview.png" alt="logo">
    </div>
    <div class="header-background">
      <img src="../assets/images/img_tablet.jpg" alt="">
    </div>
    <span class="welcome-message">Bem-vindo à Biblioteca Nova era!</span>

    <div class="login-card">
      <span class="login-title">Login</span>
      <span class="login-subtitle">Identifique-se para prosseguir</span>

      <form @submit.prevent="loginUser">
        <div class="input-group">
          <label for="email">E-mail</label>
          <input v-model="username" id="username" type="text" placeholder="Digite seu nome de usuário" required />

          <label for="password">Senha</label>
          <input v-model="password" id="password" type="password" placeholder="Digite sua senha" required />

          <!-- Ícone de senha (olho) -->
          <span class="password-toggle" @click="togglePasswordVisibility">
            <i class="fas fa-eye"></i>
          </span>

          <div class="forgot-password">
            <a href="/forgot-password">Esqueci minha Senha</a>
          </div>

          <div class="remember-me">
            <input type="checkbox" id="remember" v-model="remember" />
            <label for="remember">Lembre de mim</label>
          </div>

          <button type="submit" class="login-button">Acessar</button>
        </div>
      </form>

      <!-- Alterado para usar um @click para redirecionar -->
      <span class="register-link" @click="goToCadastro">Primeiro Acesso</span>
    </div>

    <p v-if="message" class="error-message">{{ message }}</p>
  </div>
</template>

<script>
import api from '../axios'; // Ajuste o caminho de importação conforme necessário

export default {
  data() {
    return {
      username: '',
      password: '',
      remember: false,
      message: ''
    };
  },
  methods: {
    async loginUser() {
      try {
        const response = await api.post('/auth/login', {
          username: this.username,
          password: this.password,
        });
        this.message = 'Login bem-sucedido!';
        localStorage.setItem('token', response.data.token); // Salva o token JWT
        this.$router.push('/home'); // Redireciona para a página principal
      } catch (error) {
        // A verificação do erro foi melhorada para garantir que as mensagens de erro sejam bem tratadas
        if (error.response) {
          this.message = error.response.data.error || 'Erro desconhecido ao fazer login.';
        } else {
          this.message = 'Erro ao fazer login: ' + error.message;
        }
      }
    },
    togglePasswordVisibility() {
      const passwordField = document.getElementById('password');
      const icon = document.querySelector('.password-toggle i');
      if (passwordField.type === 'password') {
        passwordField.type = 'text';
        icon.classList.remove('fa-eye');
        icon.classList.add('fa-eye-slash');
      } else {
        passwordField.type = 'password';
        icon.classList.remove('fa-eye-slash');
        icon.classList.add('fa-eye');
      }
    },
    goToCadastro() {
      // Redireciona para a página de cadastro
      this.$router.push('/cadastro');
    }
  }
};
</script>


<style scoped>
/* Estilos gerais */
* {
  box-sizing: border-box;
}
body {
  font-size: 14px;
  font-family: 'Open Sans', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f7f4f4;
}
.container {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.header-background {
  width: 100%;
  height: 395px;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.img-logo {
  position: relative;
  display: flex;
  width: 470px;
  height: 250px;
  top: -80px;
  left: -240px;
  transform: translate(-50%, -50%);
  z-index: 1;
}

img {
  width: 100%;
  height: 500px;
  position: absolute;
}

.welcome-message {
  position: absolute;
  width: 350px;
  top: 28%;
  left: 21%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 36px;
  font-weight: bold;
}

.login-card {
  width: 576px;
  top: -10%;
  background: white;
  padding: 40px;
  box-shadow: 0px 3px 20px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  position: relative;
  left: 400px;
}

.login-title {
  color: #55A8FD;
  font-size: 32px;
  margin-bottom: 10px;
}

.login-subtitle {
  color: #707070;
  font-size: 18px;
  margin-bottom: 30px;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.input-field {
  width: 100%;
  height: 52px;
  font-size: 15px;
  padding: 10px;
  border: 1px solid hsl(0, 0%, 89%);
  border-radius: 4px;
}

.password-toggle {
  position: absolute;
  top: 228px;
  right: 60px;
  color: #303942;
  cursor: pointer;
}

.forgot-password {
  text-align: right;
  margin-top: 5px;
}

.forgot-password a {
  color: #55A8FD;
  text-decoration: none;
  font-size: 12px;
}

.remember-me {
  display: flex;
  align-items: center;
  gap: 10px;
}

.login-button {
  width: 100%;
  height: 48px;
  left: 10px;
  background: #55A8FD;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  cursor: pointer;
  margin-top: 30px;
  align-items: center;
  display: flex;
  justify-content: center;
}

.register-link {
  text-align: center;
  margin-top: 20px;
}

.register-link a {
  color: #56A8FE;
  text-decoration: none;
  font-size: 16px;
  margin-left: 190px;
  position: relative;
  top: 10px;
}
</style>
