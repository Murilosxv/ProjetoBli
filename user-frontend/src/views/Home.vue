<template>
  <div id="app">
    <div class="app">
      <!-- Sidebar -->
      <aside class="sidebar">
        <div class="logo">
          <img src="/images/Logo-BibliNovaEra-removebg-preview.png" alt="Logo Biblioteca Virtual" class="logo-img">
        </div>
        <nav class="side-nav">
          <h3>Descubra seu Livro</h3>
          <ul>
            <template>
  <nav>
    <ul>
      <li @click="goToInicio" class="nav-link">Início</li>
      <li @click="goToAcervo" class="nav-link">Acervo</li>
    </ul>
  </nav>
  <router-view />
</template>

          </ul>
          <h3>Seu Acervo</h3>
          <ul>
            <li @click="goToBookCrud" class="nav-link">Seus Livros</li>
            <li><a></a></li>
          </ul>
        </nav>
      </aside>
      
      <!-- Main Content -->
      <main class="main-content">
        <header class="header">
          <div class="user-menu">
            <img src="../assets/images/logo-perfil.png" alt="User" id="info-image" class="user-avatar">
            <div id="info-popup" class="popup">
              <p><strong>Nome:</strong> <span id="name"></span></p>
              <p><strong>E-mail:</strong> <span id="email"></span></p>
              <ul>
                <li><a href="adm.html">Administração</a></li>
              </ul>
            </div>
          </div>
        </header>
        
        <!-- Sugestões de Leitura -->
        <section class="book-section">
          <div class="section-header">
            <h5>Sugestões de leitura</h5>
            <div class="carousel-controls">
              <button class="carousel-btn prev">&lt;</button>
              <button class="carousel-btn next">&gt;</button>
            </div>
          </div>
          <div class="book-carousel">
            <div class="book-card" v-for="book in suggestedBooks" :key="book.title">
              <img :src="book.image" :alt="book.title" class="book-cover">
              <div class="book-info">
                <h3>{{ book.title }}</h3>
                <p class="author">{{ book.author }}</p>
                <div class="rating">
                  <span class="star" v-for="n in book.rating" :key="n">★</span>
                  <span class="star" v-for="n in 5 - book.rating" :key="5 + n">☆</span>
                </div>
              </div>
            </div>
          </div>
        </section>
        
        <!-- Adicionados Recentemente -->
        <section class="book-section">
          <div class="section-header">
            <h2>Adicionados Recentemente</h2>
            <div class="carousel-controls">
              <button class="carousel-btn prev">&lt;</button>
              <button class="carousel-btn next">&gt;</button>
            </div>
          </div>
          <div class="book-carousel2">
            <div class="book-card" v-for="book in recentBooks" :key="book.title">
              <img :src="book.image" :alt="book.title" class="book-cover">
              <div class="book-info2">
                <h3>{{ book.title }}</h3>
                <p class="author">{{ book.author }}</p>
                <div class="rating">
                  <span class="star" v-for="n in book.rating" :key="n">★</span>
                  <span class="star" v-for="n in 5 - book.rating" :key="5 + n">☆</span>
                </div>
              </div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      suggestedBooks: [
        {
          image: '../assets/images/calculo-integral.png',
          title: 'Calculo Integral',
          author: 'Lorem Ipsum',
          rating: 4
        },
        // Adicione mais livros aqui
      ],
      recentBooks: [
        {
          image: '../assets/images/calculo-integral.png',
          title: 'Calculo Integral',
          author: 'Lorem Ipsum',
          rating: 4
        },
        // Adicione mais livros aqui
      ]
    };
  },
  methods: {
  goToInicio() {
    this.$router.push('/home');
  },
  goToBookCrud() {
    this.$router.push('/bookCrud');
  },
  goToAcervo() {
    this.$router.push('/acervo');
  }
}
}

</script>

<style>
:root {
  --primary-color: #0066cc;
  --secondary-color: #f5f5f7;
  --text-primary: #ffffff;
  --text-dif: #575757;
  --text-secondary: #464646;
  --sidebar-width: 250px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  background-color: var(--secondary-color);
  color: var(--text-primary);
  
  /* Impede a rolagem horizontal */
  
}

.app {
  display: flex;
  min-height: 100vh;
}

/* Sidebar Styles */
.sidebar {
  width: var(--sidebar-width);
  background-color: white;
  padding: 2rem;
  position: fixed;
  height: 100vh;
  box-shadow: 2px 0 4px rgba(0, 0, 0, 0.1);
}

.logo {
  margin-bottom: 2rem;
}

.logo-img {
  width: 150px;
  height: auto;
}

.side-nav h3 {
  font-size: 0.9rem;
  color: var(--text-secondary);
  margin: 1.5rem 0 0.5rem;
}

.side-nav ul {
  list-style: none;
}

.nav-link {
  /* Aqui da para ver a primeira cor que aparece nos link da nav */
  color: var(--text-dif);
  text-decoration: none;
  padding: 0.5rem 0;
  display: block;
  transition: color 0.3s;
}

.nav-link:hover {
  /* Aqui da para ver a segunda cor que aparece nos link da nav */
  color: var(--primary-color);
}

.main-content {
  background-image: url('../assets/images/fundo.jpg');
  background-size: cover;
  /* Faz a imagem de fundo cobrir toda a área */
  background-repeat: no-repeat;
  background-position: center;
  /* Centraliza a imagem de fundo */
  width: 100%;
  /* Define a largura como 100% do contêiner */
  height: 700px;
  /* Define a altura fixa */
  margin-left: var(--sidebar-width);
  flex: 1;
  padding: 2rem;
}


.header {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 2rem;
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 1;
}

.profile-container {
  text-align: center;
}

.profile-img {
  border-radius: 50%;
  cursor: pointer;
  width: 100px;
  height: 100px;
  border: 3px solid #4CAF50;
  transition: transform 0.3s ease;
}

.profile-img:hover {
  transform: scale(1.1);
}

/* Estilo do popup */
.popup {
  position: absolute;
  top: 10px;
  left: 93%;
  background: rgba(31, 29, 29, 0.11);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  padding: 20px;
  border-radius: 8px;
  display: none;
  z-index: 999;
  width: 250px;
  text-align: center;
}

.popup.active {
  display: block;
}

/* Estilo dos textos */
.popup p {
  margin: 10px 0;
}

/* Estilo da barra de informações */
.info-bar {
  display: none;
  position: fixed;
  top: 20%;
  left: 50%;
  transform: translateX(-50%);
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  width: 300px;
  text-align: center;
  z-index: 1000;
}

.info-bar h2 {
  margin-top: 0;
}

.info-bar p {
  margin: 10px 0;
}

.info-bar button {
  background-color: #f44336;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.info-bar button:hover {
  background-color: #e53935;
}


/* Book Section Styles */
.book-section {
  margin-bottom: 3rem;
}

h5 {
  color: #f5f5f7;
  font-size: 27px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.0rem;

}

.section-header h2 {
  font-size: 1.5rem;
  font-weight: 600;
}

.subtitle {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

.book-card {
  width: 250px;
  /* Define a largura do elemento como 250 pixels */
  background-color: rgba(255, 255, 255, 0);
  /* Define a cor de fundo como transparente */
  border-radius: 10px;
  /* Aplica bordas arredondadas */
  text-align: center;
  /* Centraliza o texto */
  padding: 15px;
  /* Adiciona um espaço interno */
  margin: 50px;
  /* Define uma margem externa */
  transition: transform 0.3s, box-shadow 0.3s;
  /* Efeito de transição para hover */
  scroll-snap-align: center;
  /* Faz com que os itens se alinhem no centro */
}

.book-card2 {
  width: 250px;
  /* Define a largura do elemento como 250 pixels */
  background-color: rgba(255, 255, 255, 0);
  /* Define a cor de fundo como transparente */
  border-radius: 10px;
  /* Aplica bordas arredondadas */
  text-align: center;
  /* Centraliza o texto */
  padding: 15px;
  /* Adiciona um espaço interno */
  margin: 20px;
  /* Define uma margem externa */
  transition: transform 0.3s, box-shadow 0.3s;
  /* Efeito de transição para hover */
  scroll-snap-align: center;
  /* Faz com que os itens se alinhem no centro */
  color: var(--text-dif);
}

.book-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.book-cover {
  width: 101%;
  /* Faz a imagem ocupar toda a largura do card */
  height: 300px;
  /* Ajusta a imagem para preencher o espaço sem distorção */
  object-position: center;
  /* Centraliza a imagem */
}

.book-info {
  padding: 1rem;
}

.book-info2 {
  padding: 1rem;
  color: var(--text-dif);
}

.book-info h3 {
  /* titulo */
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

.author {
  color: var(--text-secondary);
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.rating {
  color: #ffd700;
}

h2 {
  color: var(--text-dif);
}

/* Controle do carrossel */
/* Contêiner do carrossel */
/* Controle do carrossel */
.carousel-controls {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
}

.carousel-btn {
  background: white;
  border: 1px solid #ddd;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s;
}

.carousel-btn:hover {
  background-color: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}

.book-carousel {
  display: flex;
  overflow-x: auto;
  scroll-behavior: smooth;
  gap: 1rem;
  padding: 1rem;
  width: 100%;
  /* Ajuste conforme necessário */
}

/* Carousel Styles */
.book-carousel {
  display: flex;
  gap: 1.5rem;
  /* Espaço entre os itens */
  overflow-x: auto;
  /* Permite o scroll horizontal */
  scroll-snap-type: x mandatory;
  /* Faz com que o carrossel 'pule' entre os itens */
  -webkit-overflow-scrolling: touch;
  /* Melhor desempenho em dispositivos móveis */
}

.book-carousel2 {
  display: flex;
  gap: 1.5rem;
  /* Espaço entre os itens */
  overflow-x: auto;
  /* Permite o scroll horizontal */
  scroll-snap-type: x mandatory;
  /* Faz com que o carrossel 'pule' entre os itens */
  -webkit-overflow-scrolling: touch;
  /* Melhor desempenho em dispositivos móveis */
}
</style>
