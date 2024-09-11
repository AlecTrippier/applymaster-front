<template>
    <div>
      <h1>{{ message }}</h1>
      <button @click="fetchData">Fetch Data</button>

      <div>
        <ul>
          <li v-for="item in items" :key="item.id">{{ item.name }}</li>
        </ul>
      </div>
    </div>
  </template>

  <script>
  import axios from 'axios';

  export default {
    data() {
      return {
        message: '',
        items: []  // items データプロパティを追加
      };
    },
    methods: {
      async fetchData() {
        try {
          // APIからメッセージを取得
          const response = await axios.get('http://localhost:8000/api/data');
          this.message = response.data.message;

          // APIからアイテムリストを取得
          const itemsResponse = await axios.get('http://localhost:8000/api/items');
          this.items = itemsResponse.data;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      }
    }
  };
  </script>

  <style scoped>
  /* スタイルをここに追加 */
  </style>

