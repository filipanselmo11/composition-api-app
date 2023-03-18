<script setup>
import { ref, computed } from 'vue';

const header = ref('Shopping List App')

// const items = ref({
//   'item-1':{ id: 1, label: '10 party hats', purchased: true, highPriority: false },
//   'item-2':{ id: 2, label: '2 board games', purchased: true, highPriority: false },
//   'item-3':{ id: 3, label: '20 cups', purchased: true, highPriority: false },
// })

const characterCount = computed(() => {
  return newItem.value.length
})
const items = ref([
])


const reverseItems = computed(() => {
  return [...items.value].reverse() //reverse Array
})

const edit = ref(false)

const newItem = ref('')
const newItemHighPriority = ref(false)

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem, highPriority: newItemHighPriority.value })
  newItem.value = ''
  newItemHighPriority.value = ''
}

const doEdit = (e) => {
  edit.value = e
  newItem.value = ''
}

const togglePurchased = (item) => {
  item.purchased = !item.purchased
}
</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="edit" class="btn" @click="doEdit(false)">
      Cancel
    </button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">
      Add Item
    </button>
  </div>
  <a :href="newItem">Dynamic Link</a>
  <form class="add-item-form" @submit.prevent="saveItem" v-if="edit">
    <input v-model.lazy="newItem" type="text" placeholder="Add an item">
    <label>
      <input type="checkbox" @keyup.enter="saveItem" v-model="newItemHighPriority">
      High Priority
    </label>
    <button :disabled="newItem.length < 5" class="btn btn-primary">
      Save
    </button>
  </form>
  <p class="counter">
    {{ characterCount }}/200  
  </p>
  <ul>
    <li
      v-for="item in reverseItems"
      @click="togglePurchased(item)"
      :key="item.id"
      class="static-class"
      :class="[
        {strikeout: purchased},
        {priority: highPriority}
      ]">{{ label }}</li>
  </ul>

  <p v-if="!items.length"> ...</p>
</template>

<style></style>