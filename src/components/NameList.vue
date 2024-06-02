<template>
    <div class="container">
      <div class="content">
        <h1>TEGUH CRUD T6</h1>
        <input v-model="newName" placeholder="Enter name" />
        <button @click="addName">Add Name</button>
        <ul>
          <li v-for="name in names" :key="name.id">
            {{ name.name }}
            <button @click="deleteName(name.id)">Delete</button>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  const JSONBIN_URL = 'https://api.jsonbin.io/v3/b/6658ab95ad19ca34f871b940';
  const JSONBIN_SECRET_KEY = '$2a$10$DAyUrkEOEvYb0od5x9pA8OyfLfBiXtTcL03DHnhjlHY06HDACnJp.';
  
  export default {
    data() {
      return {
        newName: '',
        names: []
      };
    },
    methods: {
      async fetchNames() {
        try {
          const response = await axios.get(`${JSONBIN_URL}/latest`, {
            headers: {
              'X-Master-Key': JSONBIN_SECRET_KEY
            }
          });
          this.names = response.data.record.names;
        } catch (error) {
          console.error('Error fetching names:', error);
        }
      },
      async addName() {
        if (this.newName.trim() === '') return;
        try {
          this.names.push({ id: Date.now(), name: this.newName });
          await axios.put(JSONBIN_URL, { names: this.names }, {
            headers: {
              'Content-Type': 'application/json',
              'X-Master-Key': JSONBIN_SECRET_KEY
            }
          });
          this.newName = '';
        } catch (error) {
          console.error('Error adding name:', error);
        }
      },
      async deleteName(id) {
        try {
          this.names = this.names.filter(name => name.id !== id);
          await axios.put(JSONBIN_URL, { names: this.names }, {
            headers: {
              'Content-Type': 'application/json',
              'X-Master-Key': JSONBIN_SECRET_KEY
            }
          });
        } catch (error) {
          console.error('Error deleting name:', error);
        }
      }
    },
    created() {
      this.fetchNames();
    }
  };
  </script>
  
  <style>
  body {
    font-family: 'Arial', sans-serif;
    background-color: #f0f2f5;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  .container {
    width: 400px;
    padding: 20px;
    background-color: rgba(255, 255, 255, 0.8); /* Made the background transparent */
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  .content {
    text-align: center;
  }
  
  h1 {
    margin-bottom: 20px;
    color: #333;
    font-size: 24px;
  }
  
  input {
    width: calc(100% - 20px);
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 16px;
  }
  
  button {
    padding: 10px 20px;
    background-color: #007bff;
    border: none;
    border-radius: 5px;
    color: white;
    font-size: 16px;
    cursor: pointer;
    margin-bottom: 10px;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  li button {
    background-color: #dc3545;
    border: none;
    border-radius: 5px;
    color: white;
    padding: 5px 10px;
    cursor: pointer;
  }
  
  li button:hover {
    background-color: #c82333;
  }
  </style>
  