<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Crypto Prices</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <!-- Tombol untuk mengambil data -->
      <ion-button expand="block" @click="fetchCryptoData">Get Data</ion-button>

      <!-- Tabel untuk menampilkan data -->
      <div class="table-container">
        <table>
          <thead>
            <tr>
              <th>Nama</th>
              <th>Simbol</th>
              <th>Harga USD</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="crypto in cryptoData" :key="crypto.id">
              <td>{{ crypto.name }}</td>
              <td>{{ crypto.symbol }}</td>
              <td>{{ crypto.price_usd }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Pesan jika data belum tersedia -->
      <ion-text v-if="cryptoData.length === 0" class="ion-text-center">
        <p>No Data Available</p>
      </ion-text>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      cryptoData: [], // Array untuk menyimpan data crypto
    };
  },
  methods: {
    async fetchCryptoData() {
      const url = "https://api.coinlore.net/api/tickers/";
      try {
        const response = await axios.get(url);
        this.cryptoData = response.data.data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
  },
};
</script>

<style>
/* Gaya untuk tabel */
.table-container {
  padding: 16px;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
  background-color: #ffffff; /* Pastikan tabel juga memiliki latar belakang putih */
}

thead {
  background-color: #f1f1f1; /* Warna latar belakang untuk header tabel */
}

tbody tr:hover {
  background-color: #f9f9f9; /* Warna latar saat hover */
}

th, td {
  padding: 12px;
  border: 1px solid #ddd;
}

th {
  font-weight: bold;
  text-align: left;
}

tbody tr:hover {
  background-color: #f9f9f9;
}
</style>
