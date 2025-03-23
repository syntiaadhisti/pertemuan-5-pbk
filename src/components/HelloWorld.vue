<script setup>
import { ref, computed, reactive, watch, onMounted, onUnmounted, onUpdated } from 'vue';

console.info('Hello syntia');

const hello = ref("Hello syntia");
const userInput = ref(""); 
const tes = ref("Ini tes");
const warna = ref('blue');
const tebal = ref('bold');
const usia = ref(0);

const daftar_film = ref([
  { judul: "Doraemon", tahun: 2011 },
  { judul: "Snow White", tahun: 2001 },
  { judul: "Beauty and the Beast", tahun: 2023 }
]);

const Nama_User = ref('');

const greetingMessage = computed(() => {
  console.log("fungsi greetingMessage digunakan");
  return `Halo' ${Nama_User.value}`;
});

const counter = ref(0);

function count() {
  counter.value++;
  console.log("fungsi count digunakan");
}

const obj = reactive({ count: 0 });

function tambah() {
  obj.count++;
}

watch(() => obj.count, (newValue, oldValue) => {
  console.log('obj.count changed:', newValue, oldValue);
});

const inputTes = ref(null);

onMounted(() => {
  console.log("The component is now mounted.");
});

onUnmounted(() => {
  console.log("The component is now unmounted.");
});

onUpdated(() => {
  console.log("The component is now updated.");
});

function showAlert() {
  window.alert('Tombol diklik!');
}

function tampilkan() {
  if (inputTes.value) {
    console.log("Isi input:", inputTes.value.value);
  }
}
</script>

<template>
  <h1 class="hello">{{ hello }}</h1>
  <div v-html="hello"></div>
  <input v-model="userInput" type="text" placeholder="Enter your name">
  <input type="number" v-model="usia" placeholder="Masukkan usia anda" />
  
  <div>
    <p>Usia anda: {{ usia }}</p>
    <p v-if="usia < 17">Anda masih anak-anak</p>
    <p v-else-if="usia >= 17 && usia < 60">Anda sudah dewasa</p>
    <p v-else>Anda sudah tua</p>
  </div>
  
  <p>Anda mengetik: {{ userInput }}</p>
  <div>{{ tes }}</div>
  <button @click="() => tes = 'Tes telah berubah!'">Change</button>
  
  <button @click="showAlert">Klik Aku</button>
  
  <div :style="{ color: warna, fontWeight: tebal }">{{ tes }}</div>
  
  <hr>
  <h1>Daftar Film</h1>
  <ul>
    <li v-for="item in daftar_film" :key="item.judul">
      {{ item.judul }} - Tahun {{ item.tahun }}
    </li>
  </ul>

  <input v-model="Nama_User" type="text" placeholder="Masukkan Nama">
  <h2>{{ greetingMessage }}</h2><br>

  <button @click="count">Count is {{ counter }}</button>

  <button @click="tambah">Tambah Count</button>
  <p>Nilai obj.count: {{ obj.count }}</p>

  <h1>Tes Template Refs</h1>
  <input ref="inputTes" type="text" />
  <button @click="tampilkan">Tampilkan</button>
</template>