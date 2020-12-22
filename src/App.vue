<template>
  <div class="grid-container">
    <div class="Title">
      <h1>TO DO LIST</h1>
    </div>
    <div class="Label container">
      <span class="label-new">Add new task:</span>
    </div>
    <div class="Input container ">
      <input class="input-text" v-model="newItem" name="newItem" />
    </div>
    <div class="Add container">
      <button class="add" @click="addNewItem">Add</button>
    </div>

    <div class="Reset container">
      <button class="add delete" @click="removeAllItems">RESET</button>
    </div>
    <div class="Mark container">
      <button class="add Mark" @click="markAllDone">Mark All Done</button>
    </div>

    <ul class="List container">
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
          {{ todo.content }}
        </h3>
        <button @click="deleteItem(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const newItem = ref('')
    const todos = ref([])

    function addNewItem() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newItem.value,
      })
      newItem.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function deleteItem(index) {
      todos.value.splice(index, 1)
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true))
    }

    function removeAllItems() {
      todos.value = []
    }

    return {
      todos,
      newItem,
      addNewItem,
      toggleDone,
      deleteItem,
      markAllDone,
      removeAllItems,
    }
  },
}
</script>

<style>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  gap: 0px 0px;
  grid-template-areas:
    'Title Title Title Title'
    'Label Input Input Add'
    '. . Mark Reset'
    'List List List List';
}

.Input {
  grid-area: Input;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.Label {
  grid-area: Label;
}
.input-text {
  font-size: 17px;
  width: 100%;
  padding: 10px 5px 10px 40px;
  display: block;
  border: 1px solid #ededed;
  border-radius: 4px;
  transition: 0.2s ease-out;
  color: darken(#ededed, 30%);
}
input-text:focus {
  padding: 10px 5px 10px 10px;
  outline: 0;
  border-color: #ff7052;
}

.Add {
  grid-area: Add;
}

.Title {
  grid-area: Title;
}

.Reset {
  grid-area: Reset;
}

.List {
  grid-area: List;
}

.Mark {
  grid-area: Mark;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}

.add {
  background-color: #44c767;
  border-radius: 28px;
  border: 1px solid #18ab29;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 17px;
  padding: 16px 31px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #2f6627;
}
.add hover {
  background-color: #5cbf2a;
}
.add:active {
  position: relative;
  top: 1px;
}

.label-new {
  align-self: center;
  margin: 0 auto;
  top: 50%;
  font-size: 20px;
  font-weight: 700;
}

.delete{
  background-color: rgb(255,0,0);
}

.delete:hover{
  
  background-color: rgb(255,0,0);
  opacity: 90%;

}

</style>
