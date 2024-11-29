<template>
  <div>
    <h1>Coinlore API Data</h1>
    <button @click="fetchData">Get Data</button> <!-- Tombol untuk update data -->
    <table border="1">
      <thead>
        <tr>
          <th>Name</th>
          <th>Symbol</th>
          <th>Price (USD)</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="coin in coins" :key="coin.id">
          <td>{{ coin.name }}</td>
          <td>{{ coin.symbol }}</td>
          <td>{{ coin.price_usd }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import api from '../services/api'; // Pastikan Anda sudah punya service API

export default {
  data() {
    return {
      coins: [], // Data API
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await api.get('/tickers/');
        this.coins = response.data.data; // Perbarui data dari API
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
  },
  async created() {
    await this.fetchData(); // Ambil data saat komponen dimuat
  },
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f4f4f4;
}

button {
  padding: 10px 20px;
  margin-bottom: 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
