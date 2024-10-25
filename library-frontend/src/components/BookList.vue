<template>
    <div class="booklist-container">
      <h1>Lista de Livros</h1>
      <ul class="book-list">
        <li v-for="book in books" :key="book.id" class="book-item">
          <span class="book-title">{{ book.title }} - {{ book.author }} ({{ book.year }})</span>
          <div class="button-group">
            <button @click="editBook(book)" class="edit-button">Editar</button>
            <button @click="deleteBook(book._id)" class="delete-button">Excluir</button>
          </div>
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
      };
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