<template>
  <div class="booklist-container">
    <h1>Lista de Livros</h1>
    <ul class="book-list">
      <li v-for="book in filteredBooks" :key="book.id" class="book-item">
        <!-- Exibe a imagem do livro se estiver disponível -->
        <img :src="book.image ? `http://localhost:3000${book.image}` : ''" alt="Capa do livro" v-if="book.image" class="book-image" />
        
        <!-- Exibe as informações do livro -->
        <div class="book-info">
          <!-- Título do livro -->
          <span class="book-title">Title: {{ book.title }}</span>
          <!-- Autor do livro -->
          <span class="book-author">Author: {{ book.author }}</span>
          <!-- Ano de publicação do livro -->
          <span class="book-year">Year: ({{ book.year }})</span>
          
          <div class="button-group">
            <button @click="editBook(book)" class="edit-button">Editar</button>
            <button @click="deleteBook(book._id)" class="delete-button">Excluir</button>
          </div>
        </div> <!-- Fechamento da tag div.book-info -->
      </li>
    </ul>
  </div>
</template>

<script>
import api from '../services/api'; // Importa o serviço API

export default {
  data() {
    return {
      books: [], // Estado local da lista de livros
      searchQuery: '', // Variável para pesquisa
    };
  },
  computed: {
    // Computed property para filtrar os livros com base na consulta de pesquisa
    filteredBooks() {
      // Filtra os livros com base no título ou autor, ignorando maiúsculas e minúsculas
      return this.books.filter((book) =>
        book.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        book.author.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    fetchBooks() { // Busca os livros do back-end
      api.getBooks().then(response => {
        this.books = response.data; // Atualiza a lista de livros
      });
    },
    deleteBook(id) { // Exclui um livro pelo ID
      api.deleteBook(id).then(() => {
        this.fetchBooks(); // Atualiza a lista após a exclusão
      });
    },
    editBook(book) { // Emite um evento para editar um livro
      this.$emit('edit-book', book);
    },
  },
  mounted() {
    this.fetchBooks(); // Busca os livros ao montar o componente
  },
};
</script>

<style scoped>
/* Estilos para o componente */
.booklist-container {
  background-color: #f4f4f4; /* Fundo cinza claro */
  color: #333; /* Texto cinza escuro */
  padding: 20px;
  border-radius: 8px;
}

h1 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 20px;
}

.book-list {
  list-style-type: none;
  padding: 0;
}

.book-item {
  display: flex; /* Flexbox para alinhar imagem e texto */
  background-color: white; /* Fundo branco para cada item */
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.book-image {
  width: 120px; /* Tamanho fixo para a imagem */
  height: 180px; /* Tamanho fixo para a imagem */
  object-fit: cover; /* Para ajustar a imagem sem distorcer */
  margin-right: 15px; /* Espaço entre a imagem e o texto */
  border-radius: 8px;
}

.book-info {
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Para distribuir o conteúdo */
}

.book-title, .book-author, .book-year {
  font-size: 1rem;
  margin: 5px 0;
}

.button-group {
  margin-top: 10px;
}

.edit-button, .delete-button {
  padding: 8px 12px;
  margin-right: 10px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}

.edit-button {
  background-color: #4CAF50; /* Verde */
  color: white;
}

.delete-button {
  background-color: #f44336; /* Vermelho */
  color: white;
}

.edit-button:hover {
  background-color: #45a049;
}

.delete-button:hover {
  background-color: #e53935;
}
</style>
