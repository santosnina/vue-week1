<template>
    <div>
      <table>
        <thead>
          <tr>
            <th scope="col">品項</th>
            <th scope="col">描述</th>
            <th scope="col">價格</th>
            <th scope="col">庫存</th>
            <th scope="col">操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in menu" :key="item.id">
            <td>
              <input v-model="item.name" />
            </td>
            <td><small>{{ item.description }}</small></td>
            <td>{{ item.price }}</td>
            <td>
              <button @click="decreaseStock(item.id)">-</button>
              {{ item.stock }}
              <button @click="increaseStock(item.id)">+</button>
            </td>
            <td>
              <button @click="updateStock(item.id, item.stock)">更新庫存</button>
              <button @click="updateItemName(item.id, item.name)">更新品項名稱</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { menu, updateStock, updateName } from '../main';
  
  const decreaseStock = (itemId) => {
    const item = menu.value.find(item => item.id === itemId);
    if (item && item.stock > 0) {
      item.stock -= 1;
    }
  };
  
  const increaseStock = (itemId) => {
    const item = menu.value.find(item => item.id === itemId);
    if (item) {
      item.stock += 1;
    }
  };
  
  const updateItemStock = (itemId, newStock) => {
    updateStock(itemId, newStock);
  };

  const updateItemName = (itemId, newName) => {
    updateName(itemId, newName);
  };
  
  </script>
  