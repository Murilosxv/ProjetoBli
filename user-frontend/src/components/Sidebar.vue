<template>
    <aside class="sidebar">
      <div class="logo">
        <img src="/images/Logo-BibliNovaEra-removebg-preview.png" alt="Logo Biblioteca Virtual" class="logo-img" />
      </div>
      <nav class="side-nav">
        <h3>Descubra seu Livro</h3>
        <ul>
          <li><a href="home.html" class="nav-link">Início</a></li>
          <li><a href="acervo.html" class="nav-link">Acervo</a></li>
        </ul>
        <h3>Seu Acervo</h3>
        <ul>
          <li><a href="Lista.html" class="nav-link">Seus downloads</a></li>
        </ul>
      </nav>
    </aside>
  </template>
  
  <script>
  export default {
    name: "Sidebar",
  };
  </script>
  
  <style scoped>
  /* Sidebar Styles */
.sidebar {
  width: var(--sidebar-width);
  background-color: white;
  padding: 32px;
  position: fixed;
  height: 100vh;
  margin-right: 200px;
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
  background-image: url('/images/fundo.jpg');
  background-size: cover;
  /* Faz a imagem de fundo cobrir toda a área */
  background-repeat: no-repeat;
  background-position: center;
  /* Centraliza a imagem de fundo */
  width: 100%;
  /* Define a largura como 100% do contêiner */
  height: 370px;
  /* Define a altura fixa */
  margin-left: var(--sidebar-width);
  flex: 1;
  padding: 2rem;
}
  </style>