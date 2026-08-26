<template>
  <div class="container">
    <h2>Form Edit Buku</h2>

    <Transition name="fade">
      <div v-if="showMessage" class="notification">
        {{ message }}
      </div>
    </Transition>

    <form @submit.prevent="handleEditSubmit" class="book-form">
      <label>Judul Buku:</label>
      <input v-model="editBookForm.title" required type="text" placeholder="Masukkan judul" />

      <label>Penulis:</label>
      <input v-model="editBookForm.author" required type="text" placeholder="Masukkan penulis" />

      <label class="checkbox-label">
        <input v-model="editBookForm.read" type="checkbox" />
        Sudah dibaca
      </label>

      <div class="button-group">
        <button type="submit">Simpan</button>
        <button type="button" @click="cancelEditBook" class="btn-cancel">Batal</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      editBookForm: {
        id: 1,
        title: 'Belajar Vue JS',
        author: 'MySkill',
        read: false
      },
      selectedBook: {
        title: 'Belajar Vue JS',
        author: 'MySkill',
        read: false
      },
      message: '',
      showMessage: false
    };
  },
  methods: {
    handleEditSubmit() {
      let readStatus = false;
      if (this.editBookForm.read) readStatus = true;

      const payload = {
        title: this.editBookForm.title,
        author: this.editBookForm.author,
        read: readStatus,
      };

      this.updateBook(payload, this.editBookForm.id);
    },

    updateBook(payload, bookID) {
      console.log("Mengirim data ke server:", payload);

      setTimeout(() => {
        this.message = 'Buku berhasil diupdate!';
        this.showMessage = true;

        setTimeout(() => {
          this.showMessage = false;
        }, 3000);
      }, 1000);
    },

    cancelEditBook() {
      this.editBookForm.title = this.selectedBook.title;
      this.editBookForm.author = this.selectedBook.author;
      this.editBookForm.read = this.selectedBook.read;

      alert("Perubahan dibatalkan");
    }
  }
};
</script>