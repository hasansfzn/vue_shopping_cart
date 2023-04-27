<script setup>
import { ref } from "vue";

// const msg = ref();
const header = ref("Shopping Cart Application");

const items = ref([
  { id: 1, label: "Nescafe 1 Pac", purchased: true, highPriority: false },
  { id: 2, label: "Ginger Tea", purchased: true, highPriority: false },
  { id: 3, label: "Baseus Headset", purchased: false, highPriority: true },
]);

const newItem = ref("");
// const priority = ref("low");
const priority = ref(false);

const addItem = () => {
  items.value.push({ label: newItem.value, id: items.value.length + 1 });
  newItem.value = "";
};

const editing = ref(false);

const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};

const togglePerchase = (e) => {
  //e.highPriority = !e.highPriority;
  e.purchased = !e.purchased;
};
</script>

<template>
  <!-- <h2 class="center">{{ msg ?? "Hello World" }}</h2>
  <input class="center" v-model="msg" /> -->
  <div class="header">
    <h2 class="center">{{ header.toLocaleUpperCase() ?? "HardCoded Cart" }}</h2>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">
      Add Item
    </button>
  </div>

  <!-- <a :href="newItem">Go to the link</a> -->
  <form class="add-item-form" @submit.prevent="addItem" v-if="editing">
    <input v-model="newItem" type="text" placeholder="Add an Item" />
    <!-- <label> <input type="radio" v-model="priority" value="low" />Low </label>
  <label> <input type="radio" v-model="priority" value="high" />High </label> -->
    <!-- <label>
    Priority:
    <select v-model="priority">
      <option value="low">Low</option>
      <option value="high">High</option>
    </select>
  </label> -->
    <label>
      <input type="checkbox" v-model="priority" />
      High Priority
    </label>
    <button
      class="btn btn-primary"
      type="submit"
      :disabled="newItem.length === 0"
    >
      Save Item
    </button>
  </form>

  <br />
  <!-- {{ priority }} -->
  <ul>
    <li
      v-for="(item, index) in items"
      :key="item.id"
      class="static-class"
      :class="[{ strikeout: item.purchased }, { priority: item.highPriority }]"
      @click="togglePerchase(item)"
    >
      {{ index + 1 }} => {{ item.label }}
    </li>
  </ul>
  <p v-if="!items.length">No items to show!</p>
</template>

<style>
.center {
  text-align: center;
}
</style>
