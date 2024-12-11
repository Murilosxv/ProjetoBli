<template>
  <div class="bookform-container">
    <form @submit.prevent="handleSubmit" class="form">
      <h2>{{ book._id ? 'Editar Livro' : 'Adicionar Novo Livro' }}</h2>
      <input v-model="book.title" placeholder="Título" required class="form-input" />
      <input v-model="book.author" placeholder="Autor" required class="form-input" />
      <input v-model="book.year" placeholder="Ano de Publicação" required type="number" class="form-input" />
      
      <div class="file-input-container">
        <input type="file" id="file-upload" @change="handleFileChange" class="file-upload" />
        <label for="file-upload" class="file-upload-label">Escolha a Imagem</label>
        <div v-if="imageChosen" class="image-chosen-message">Imagem escolhida!</div>
      </div>

      <button type="submit" class="submit-button">{{ book._id ? 'Atualizar' : 'Adicionar' }}</button>
    </form>
  </div>
</template>

<script>
import api from '@/services/api'; // Importa o serviço API para fazer requisições

export default {
  props: ['bookToEdit'], // Recebe o livro a ser editado como uma prop
  data() {
    return {
      book: this.bookToEdit || { title: '', author: '', year: null, image: null, _id: null }, // Inicializa os dados do livro
      selectedImage: null,
      imageChosen: false, // Inicializa o estado de imagem escolhida
    };
  },
  watch: {
    bookToEdit: {
      immediate: true,
      handler(newValue) {
        if (newValue) {
          this.book = { ...newValue }; // Atualiza os dados do livro para edição
        } else {
          this.resetForm(); // Se não houver livro para editar, reseta o formulário
        }
      },
    },
  },
  methods: {
    // Função chamada quando o arquivo de imagem é alterado
    handleFileChange(event) {
      this.selectedImage = event.target.files[0]; // Armazena a imagem selecionada
      this.imageChosen = !!this.selectedImage; // Marca a imagem como escolhida se houver
    },
    handleSubmit() {
      const formData = new FormData();
      formData.append('title', this.book.title);
      formData.append('author', this.book.author);
      formData.append('year', this.book.year);

      // Se uma imagem foi selecionada, adiciona ao FormData
      if (this.selectedImage) {
        formData.append('image', this.selectedImage);
      }

      // Verifica se o livro tem um _id (para atualização) ou se é um novo livro
      if (this.book._id) {
        api.updateBook(this.book._id, formData).then(() => {
          this.$emit('book-updated'); // Emite evento após atualização
          this.resetForm(); // Reseta o formulário
        });
      } else {
        api.addBook(formData).then(() => {
          this.$emit('book-added'); // Emite evento após adicionar
          this.resetForm(); // Reseta o formulário
        });
      }
    },
    // Função para resetar os dados do formulário
    resetForm() {
      this.book = { title: '', author: '', year: null, image: null, _id: null };
      this.selectedImage = null; // Reseta a imagem selecionada
      this.imageChosen = false; // Reseta o estado de imagem escolhida
    },
  },
};
</script>

<style scoped>
/* Estilos para o componente do formulário */
.bookform-container {
  background-color: #ffffff; /* Fundo branco para o formulário */
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 30px;
  max-width: 500px;
  margin: 0 auto;
}

h2 {
  font-size: 1.5rem;
  text-align: center;
  color: #333;
  margin-bottom: 20px;
}

.form {
  display: flex;
  flex-direction: column;
}

.form-input {
  padding: 10px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1rem;
}

.file-input-container {
  display: flex;
  flex-direction: column;
  margin: 10px 0;
}

.file-upload {
  margin-bottom: 10px;
}

.file-upload-label {
  cursor: pointer;
  color: #007bff;
  font-size: 0.9rem;
}

.image-chosen-message {
  font-size: 0.9rem;
  color: #28a745;
  margin-top: 5px;
}

.submit-button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1rem;
  margin-top: 20px;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #45a049;
}
</style>
