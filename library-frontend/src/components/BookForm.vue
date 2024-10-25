<template>
  <div class="bookform-container">
    <form @submit.prevent="handleSubmit">
      <input v-model="book.title" placeholder="Título" required />
      <input v-model="book.author" placeholder="Autor" required />
      <input v-model="book.year" placeholder="Ano" required />
      <button type="submit">{{ book._id ? 'Atualizar' : 'Adicionar' }}</button>
    </form>
  </div>
</template>
 
<script>
import api from '@/services/api'; // Importa o serviço API para fazer requisições
 
export default {
  props: ['bookToEdit'], // Recebe o livro a ser editado como uma prop
  data() {
    return {
      book: this.bookToEdit || { title: '', author: '', year: null }, // Inicializa os dados do livro
    };
  },
  watch: {
    bookToEdit: {
      immediate: true,
      handler(newVal) {
        this.book = newVal || { title: '', author: '', year: null }; // Atualiza os dados quando a prop mudar
      },
    },
  },
  methods: {
    handleSubmit() {
      if (this.book._id) {
        api.updateBook(this.book._id, this.book).then(() => {
          this.$emit('book-updated'); // Emite um evento quando o livro é atualizado
        });
      } else {
        api.addBook(this.book).then(() => {
          this.$emit('book-added'); // Emite um evento quando um novo livro é adicionado
        });
      }
    },
  },
};
</script>