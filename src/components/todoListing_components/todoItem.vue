<template>
  <!-- <div>Todo</div>
  <div class="todo">{{ todoArray.length > 0 }}</div> -->

  <section class="todo-list-container">
    <ul v-if="todoArray.length > 0" class="todo-existing-list-container">
      <li
        v-for="todo in todoArray"
        :key="todo.dateAdded"
        class="todo-existing-item-card"
      >
        <div class="todo-existing-props-container">
          <div class="todo-existing-checkbox-container">
            <input type="checkbox" />
          </div>
          <div class="todo-existing-props-body-container">
            <p class="todo-existing-title" v-if="isEdit">{{ todo.title }}</p>
            <input
              class="todo-input"
              v-if="!isEdit"
              v-model="todo.title"
            />
            <p v-if="isEdit" class="todo-existing-status">
              Status: {{ todo.selectedStatus }}
            </p>
            <select
              class="todo-select"
              id="todo-status"
              aria-label="Status element to choose to do status"
              name="todo-status"
              v-model="todo.selectedStatus"
              autocomplete="off"
              v-if="!isEdit"
            >
              <option disabled value="">Select Status</option>
              <option value="Incomplete">Incomplete</option>
              <option value="Complete">Complete</option>
            </select>

            <p class="todo-existing-date">{{ todo.dateAdded }}</p>
          </div>
        </div>

        <div class="todo-existing-props-button">
          <button v-if="isEdit" type="button" @click="handleEdit(todo)">
            Edit
          </button>
          <button
            v-if="!isEdit"
            type="submit"
            @click="handleSubmitEdit(todo)"
          >
            Submit
          </button>
          <button type="button" @click="handleDelete(`${todo.dateAdded}`)">
            Delete
          </button>
        </div>
      </li>
    </ul>
    <div class="todo-no-item-container" v-else>
      <p class="todo-no-item-display">
        No todo item. Add item to see list here.
      </p>
    </div>
  </section>
</template>

<script>
// import TodoForm from "../todoForm.vue";

export default {
  // components: { TodoForm },
  props: ["todoArray"],
  data() {
    return {
      isEdit: true,
    };
  },
  methods: {
    handleEdit(todoObject) {
      this.isEdit = !this.isEdit;
    },
    handleSubmitEdit(todoObject) {
      this.isEdit = !this.isEdit;
      this.$emit("todoObject", todoObject);
    },
    handleDelete(todoDate) {
      this.$emit("todoDate", todoDate);
    },
  },
  emits: ["todoDate", "todoObject"],
};
</script>

<style scoped>
.todo-list-container {
  color: rgb(48, 48, 48);
  background: transparent;
  padding: 0;
}
.todo-existing-item-card {
  width: 100%;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  background-color: #f1f1f1;
  border-radius: 0.375rem;
  box-shadow: 0 0 3px 0.5px var(--appHeaderColor);
  margin-bottom: 1rem;
  padding: 0.75rem;
}
.todo-existing-props-container {
  display: flex;
  gap: 0.875rem;
}
.todo-existing-props-body-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 0.25rem;
}
.todo-existing-checkbox-container input:checked {
  fill: var(--appHeaderColor);
  outline: 2px solid var(--appHeaderColor);
  transition: all 500ms ease-in;
}
.todo-existing-title {
  font-size: 1.125rem;
  font-weight: 600;
  font-style: normal;
  word-break: break-all;
  overflow: auto;
}
.todo-existing-status {
  font-size: 0.875rem;
  font-weight: 400;
  font-style: normal;
}
.todo-existing-date {
  font-size: 0.625rem;
  font-weight: 300;
  font-style: normal;
  padding: 0.25rem;
  background-color: var(--appBackgroundColor);
  border-radius: 0.375rem;
}
.todo-existing-props-button {
  display: flex;
  text-align: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.875rem;
}
.todo-existing-props-button button {
  font-size: 0.875rem;
  font-weight: 400;
  font-style: normal;
  border: none;
  padding: 0.375rem;
  border-radius: 0.25rem;
  background-color: var(--OpacOffBlack1);
}
.todo-existing-props-button button:hover {
  background-color: var(--OpacOffBlack2);
}
.todo-existing-props-button button:focus {
  background-color: var(--OpacOffBlack2);
  outline: 2px solid #005bd3;
  transition: all 200ms ease-in;
}
.todo-no-item-display {
  display: flex;
  text-align: center;
  justify-content: center;
  font-size: 0.875rem;
}
.todo-no-item-container {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f1f1f1;
  padding: 2rem;
  border-radius: 0.375rem;
  box-shadow: 0 0 3px 0.5px var(--appHeaderColor);
  margin-bottom: 1rem;
}
.todo-input, .todo-select {
  font-size: 0.875rem;
  font-weight: 300;
  padding: 0.375rem;
  margin-bottom: 0.125rem;
  border-radius: 0.25rem;
  background-color: #dbdbdb;
  border: 1px solid #828282;
}
.todo-input:focus, .todo-select:focus {
  border: none;
  outline: 2px solid #005BD3;
  transition: all 200ms ease-in;
}
.todo-input::placeholder {
  color: var(--OpacBlack);
}
.todo-select option {
  color: var(--OpacBlack);
}

</style>
