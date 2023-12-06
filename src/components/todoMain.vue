<template>
  <div class="todo-main-wrapper">
    <section class="subheader-add-todo-container">
      <button class="subheader-add-todo-btn" @click="handleOpenForm">
        Add Todo
      </button>
    </section>
    <TodoItem :todoArray="todoArray" @todoObject="handleEditTodo"  @todoDate="handleDeleTodo" />
    <TodoForm
      :isFormOpen="isFormOpen"
      :isEdit="isEdit"
      :todoObjectToEdit="todoObjectToEdit"
      :todoArray="todoArray"
      @todo-object="onSubmitForm"
      @handleCloseForm="handleCloseForm"
    />
  </div>
</template>

<script>
import TodoForm from "./todoForm.vue";
import TodoItem from "./todoListing_components/todoItem.vue";
// import TodoForm from "./components/todoForm.vue";
import { index } from '../../../../TypeScript-Node-Starter/src/controllers/home';

export default {
  components: { TodoItem, TodoForm },
  data() {
    return {
      isFormOpen: false,
      isEdit: false,
      todoArray: [],
      todoObjectToEdit: null
    };
  },
  methods: {
    onSubmitForm(todoObject) {
      this.isFormOpen = !this.isFormOpen;
      this.todoArray.push(todoObject);
        },
    handleOpenForm() {
      this.isFormOpen = !this.isFormOpen;
    },
    handleCloseForm() {
      this.isFormOpen = !this.isFormOpen;
      this.isEdit = false
    },
    handleEditTodo(todoObject){
        console.log(todoObject)
        this.todoArray.forEach((todo)=>{
            if(todo.dateAdded === todoObject.dateAdded){
                todo.title = todoObject.title;
                todo.selectedStatus = todoObject.selectedStatus;
            }
        })
    },
    handleDeleTodo(todoDate){
        const updatedTodoArray = this.todoArray.filter((todo) => todo.dateAdded !== `${todoDate}` );
        this.todoArray = updatedTodoArray;
    }
  },
};
</script>

<style scoped>
.todo-main-wrapper {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}
.subheader-add-todo-container {
  display: flex;
  justify-content: flex-start;
  margin-top: 2rem;
  margin-bottom: 0.5rem;
  padding-top: 1rem;
  padding-bottom: 1rem;
}
.subheader-add-todo-btn {
  display: flex;
  text-align: center;
  justify-content: center;
  padding: 0.5rem;
  font-size: 0.875rem;
  font-weight: 300;
  border: none;
  box-shadow: 0px 0px 3px 0.5px #171616;
  color: #181818;
  /* color: #F1F1F1; */
  border-radius: 0.25rem;
  margin-top: 0.25rem;
  background: #f1f1f1;
  outline: none;
}
.subheader-add-todo-btn:focus {
  outline: 2px solid #005bd3;
  transition: all 200ms ease-in;
}
</style>
