<script setup>
import { ref } from "vue";

const showForm = ref(false);
const newMemo = ref("");
const errorMessage = ref("");
const memos = ref([
  {
    id: "1238383883",
    memo: "makan",
    date: new Date().toLocaleDateString("en-us"),
    backgroundColor: `#${Math.floor(Math.random() * 16777275).toString(16)}`,
  },

  {
    id: "1238382883",
    memo: "minum",
    date: new Date().toLocaleDateString("en-us"),
    backgroundColor: `#${Math.floor(Math.random() * 16777275).toString(16)}`,
  },
]);

const addMemo = () => {
  if (!newMemo.value) {
    errorMessage.value = "Masukan Input";
    return;
  }
  memos.value.push({
    id: Date.now(),
    memo: newMemo.value,
    date: new Date().toLocaleDateString("en-us"),
    backgroundColor: `#${Math.floor(Math.random() * 16777275).toString(16)}`,
  });
  newMemo.value = "";
  showForm.value = false;
};

const deleteMemo = (id) => {
  memos.value = memos.value.filter((item) => item.id !== id);
};
</script>

<template>
  <div class="flex justify-between mb-5 gap-11 px-20 mx-auto items-center my-8">
    <h1 class="font-light text-5xl my-3">MEMO</h1>
    <button @click="showForm = true" class="bg-blue-500 text-white font-bold py-2 px-8 rounded hover:bg-blue-700 focus:outline-none focus:shadow-outline">+ Tambah</button>
  </div>

  <div class="flex gap-5 flex-wrap justify-center items-center">
    <div v-for="memo in memos" :key="memo.id">
      <div class="max-w-sm rounded-lg mx-auto overflow-hidden shadow-lg" :style="{ backgroundColor: memo.backgroundColor }">
        <div class="relative">
          <!-- Gambar Latar Belakang -->
          <img class="w-full h-48 object-cover" src="https://via.placeholder.com/400x300" alt="Gambar Card" />
          <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center">
            <h2 class="text-white text-3xl font-bold">{{ memo.memo }}</h2>
          </div>
        </div>

        <!-- Konten Card -->
        <div class="px-6 py-4">
          <p class="text-gray-700 text-base">Deskripsi card yang lebih panjang dengan detail lebih lengkap. Gambar latar belakang memberikan kesan visual yang lebih menarik.</p>
        </div>

        <div class="px-6 py-4">
          <p class="text-gray-700 text-base">{{ memo.date }}</p>
        </div>

        <!-- Bagian Tombol -->
        <div class="px-6 py-4 flex justify-end gap-3.5">
          <button class="bg-indigo-500 text-white font-semibold py-2 px-4 rounded-full hover:bg-indigo-700 focus:outline-none">Baca Lebih Lanjut</button>
          <button @click="deleteMemo(memo.id)" class="px-4 py-2 bg-red-500 rounded-full">Hapus</button>
        </div>
      </div>
    </div>
  </div>

  <div v-if="showForm" id="modal" class="fixed inset-0 bg-gray-500 bg-opacity-50 justify-center items-center flex">
    <!-- Modal Container -->
    <div class="bg-white p-6 rounded-lg shadow-lg max-w-sm w-full">
      <!-- Modal Header -->
      <div class="flex justify-between items-center mb-2">
        <h3 class="text-xl font-semibold text-gray-700">Modal Title</h3>
        <button @click="showForm = false" id="close-modal" class="text-gray-500 hover:text-gray-700">&times;</button>
      </div>

      <p v-if="!errorMessage" class="mb-2">Masukan Title Memo yang anda inginkan</p>
      <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>

      <!-- Modal Body -->
      <div>
        <textarea v-model="newMemo" name="memo" id="memo" cols="30" rows="10" class="w-full border-[2px] border-zinc-300"></textarea>
        <div class="mt-6 flex justify-end">
          <button id="save-btn" @click="addMemo" class="bg-blue-500 text-white px-4 py-2 rounded-lg hover:bg-blue-700">Simpan</button>
        </div>
      </div>

      <!-- Modal Footer -->
    </div>
  </div>
</template>
