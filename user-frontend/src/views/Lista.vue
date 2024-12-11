<template>
    <div class="app">
      <!-- Sidebar (barra lateral) -->
      <aside class="sidebar">
        <div class="logo">
          <img src="/images/Logo-BibliNovaEra-removebg-preview.png" alt="Logo Biblioteca Virtual" class="logo-img" />
        </div>
  
        <nav class="side-nav">
          <h3>Descubra seu Livro</h3>
          <ul>
            <li><router-link to="/home" class="nav-link">Início</router-link></li>
            <li><router-link to="/acervo" class="nav-link">Acervo</router-link></li>
          </ul>
  
          <h3>Seu Acervo</h3>
          <ul>
            <li><router-link to="/lista" class="nav-link">Seus Livros</router-link></li>
          </ul>
        </nav>
      </aside>
  
      <!-- Main Content -->
      <main class="main-content">
        <header class="header">
          <div class="user-menu">
            <img src="/images/logo-perfil.png" alt="User" id="info-image" class="user-avatar" @click="togglePopup" />
            <div v-if="showPopup" id="info-popup" class="popup">
              <p><strong>Nome:</strong> {{ user.name }}</p>
              <p><strong>E-mail:</strong> {{ user.email }}</p>
              <ul>
                <li><router-link to="/adm">Administração</router-link></li>
              </ul>
            </div>
          </div>
        </header>
  
        <div class="acervo-container">
          <h1>Seus Livros</h1>
          <p>Seu histórico de livros está disponível para consulta.</p>
  
          <div class="barra-branca">
            <div class="filtro-container">
              <div class="filtro-item" v-for="(opcoes, tipo) in filtros" :key="tipo">
                <button class="filtro-botao" @click="toggleFiltro(tipo)">{{ tipo.toUpperCase() }}</button>
                <div v-show="filtroVisivel === tipo" class="opcoes-filtro">
                  <ul>
                    <li v-for="opcao in opcoes" :key="opcao">{{ opcao }}</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
  
          <div class="book-container">
            <div
              class="book-card"
              v-for="book in books"
              :key="book.title"
              :data-categoria="book.categoria"
              :data-editora="book.editora"
              :data-nota="book.nota"
            >
              <img :src="book.image" :alt="book.title" class="book-cover" />
              <div class="book-info">
                <h3>{{ book.title }}</h3>
                <p class="author">{{ book.author }}</p>
                <div class="rating">{{ book.rating }}</div>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        user: {
          name: "Usuário",
          email: "usuario@example.com",
        },
        showPopup: false,
        filtroVisivel: null,
        filtros: {
          categoria: ["Matemática", "Educação", "Saúde", "Psicologia", "História"],
          editora: ["Editora X", "Editora Y", "Editora Z"],
          nota: ["1", "2", "3", "4", "5"],
          titulo: ["Cálculo Integral", "Didática", "Enfermagem"],
        },
        books: [
          {
            image: "../assets/images/calculo-integral.png",
            title: "Cálculo Integral",
            author: "Lorem Ipsum",
            rating: "★★★★☆",
            categoria: "matematica",
            editora: "Editora X",
            nota: 4,
          },
          {
            image: "/images/didatico-metodos.png",
            title: "Didática e Métodos de Ensino",
            author: "Maria Lucia Estivallet",
            rating: "★★★★☆",
            categoria: "educacao",
            editora: "Editora Y",
            nota: 4,
          },
          {
            image: "/images/enfermagem-unidade.png",
            title: "Enfermagem em Unidade de Saúde",
            author: "Cátia Millene Dell",
            rating: "★★★★☆",
            categoria: "saude",
            editora: "Editora Z",
            nota: 4,
          },
          {
            image: "/images/Fundamentos-Neuropsicopedagogia.png",
            title: "Fundamentos da Neuropsicopedagogia",
            author: "Raphael Moroz Teixeira",
            rating: "★★★★☆",
            categoria: "psicologia",
            editora: "Editora ABC",
            nota: 4,
          },
          {
            image: "/images/historias-memorias.png",
            title: "Histórias e Memórias",
            author: "Raphael Moroz Teixeira",
            rating: "★★★★☆",
            categoria: "historia",
            editora: "Editora XYZ",
            nota: 4,
          },
        ],
      };
    },
    methods: {
      togglePopup() {
        this.showPopup = !this.showPopup;
      },
      toggleFiltro(tipo) {
        this.filtroVisivel = this.filtroVisivel === tipo ? null : tipo;
      },
    },
  };
  </script>
  
  <style scoped>
  .app {
    display: flex;
  }
  .sidebar {
    width: 250px;
    background: #f4f4f4;
  }
  .main-content {
    flex: 1;
    padding: 20px;
  }
  .book-container {
    display: flex;
    flex-wrap: wrap;
  }
  .book-card {
    width: 200px;
    margin: 10px;
    text-align: center;
  }
  </style>
  