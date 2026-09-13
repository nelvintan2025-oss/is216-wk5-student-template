<script setup>
import { ref } from 'vue'
const items = ref(['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'])
const newItem = ref('')

// TODO: Add Code Here
function addItem(){
  if (newItem.value.trim() !== ""){
    items.value.push(newItem.value)
    newItem.value = '' //clears the input box after adding
  }
}

function removeItem(index){
  items.value.splice(index,1)
}
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->

    <ul>
      <li v-for="(item,index) in items" :key="index">
          {{ item }}
          <button @click="removeItem(index)">Delete!</button>
      </li>
    </ul>

    <!--Add items-->
    <div>
        <input v-model="newItem" type="text">
        <button @click="addItem">Add!</button>
    </div>
</template>
