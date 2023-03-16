<template>
  <div id="app">
    <h1>Todo List</h1>
    <div v-if="!isEditing">
      <form @submit.prevent="handleSubmit">
        <label for="new-todo-input"> Add Items </label>
        <input
          type="text"
          id="new-todo-input"
          name="new-todo"
          autocomplete="off"
          v-model="label"
        />
        <button type="submit">Add</button>
      </form>
    </div>
    <div v-else>
      <form @submit.prevent="handleUpdate">
        <label for="update-todo-input"> Update Items </label>
        <input
          type="text"
          id="update-todo-input"
          name="update-todo"
          autocomplete="off"
          v-model="label"
        />
        <button type="submit">Update</button>
      </form>
    </div>

    <!-- ul li -->
    <div class="border">
      <!-- <ul> -->
      <div :key="index" v-for="(data, index) in todo">
        <p>{{ data }}</p>
        <button @click="Edit(index, data)">Edit</button>
        <button @click="HandleDelete(index)">Delete</button>
      </div>
      <!-- </ul> -->
    </div>
  </div>
</template>
<script>
import { defineComponent } from "@vue/composition-api";

export default {
  data() {
    return {
      isEditing: false,
      selectedIndex: "",
      label: "",
      todo: ["22132", "1221"],
    };
  },
  methods: {
    handleSubmit() {
      console.log("handle Submit", this.label);
      this.todo.push(this.label);
    },

    Edit(index, data) {
      this.label = data;
      this.selectedIndex = index;
      this.isEditing = true;
    },

    handleUpdate(index) {
      // console.log(this.selectedIndex, "selectedIndex");
      console.log(this.label, "index");
      this.todo[this.selectedIndex] = this.label;
      //   this.todo = this.todo.splice(index, 1, this.selectedIndex);
      this.isEditing = false;
    },

    HandleDelete(index) {
      this.todo.splice(index, 1);
    },
  },
};
</script>

<style lang="scss">
.border {
  border: 1px solid black;
}
</style>
