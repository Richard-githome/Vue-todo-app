<template>
  <div class="form-wrapper" v-show="isFormOpen">
    <form id="form-container" class="form-container" @submit.prevent="onSubmitForm">
      <todoFormTitle :isEdit="$props.isEdit" />

      <label aria-labelledby="todo-input" for="todo-input" class="todo-input-label">Title</label>
      <input
        id="todo-input"
        aria-label="Input element to add to do item"
        name="todo-input"
        type="text"
        v-model="title"
        placeholder="Add a Todo item"
        class="todo-input"
        autocomplete="off"
        v-show="!$props.isEdit"
      />
      <!-- <input
        id="todo-input"
        aria-label="Input element to add to do item"
        name="todo-input"
        type="text"
        v-model="title"
        placeholder="Update Todo item"
        class="todo-input"
        autocomplete="off"
        v-show="$props.isEdit"
      /> -->

      <label aria-labelledby="todo-status" for="todo-status" class="todo-select-label">Status</label>
      <select
        class="todo-select"
        id="todo-status"
        aria-label="Status element to choose to do status"
        name="todo-status"
        v-model="status"
        autocomplete="off"
        v-show="!$props.isEdit"
      >
        <option disabled value="">Select Status</option>
        <option value="Incomplete">Incomplete</option>
        <option value="Complete">Complete</option>
      </select>
      <!-- <select
        class="todo-select"
        id="todo-status"
        aria-label="Status element to choose to do status"
        name="todo-status"
        v-model="status"
        autocomplete="off"
        v-show="$props.isEdit"
      >
        <option disabled value="">Select Status</option>
        <option value="Incomplete">Incomplete</option>
        <option value="Complete">Complete</option>
      </select> -->
      <div class="todo-form-btn-container">
        <button type="submit" aria-label="button for saving to do item" :class="['todo-form-btn', 'btn-primary']">
          {{!$props.isEdit ? "Add" : "Update"}} Todo
        </button>
        <button type="button"
          aria-label="button to cancel to do form activity"
          :class="['todo-form-btn', 'btn-secondary']"
          @click="handleCloseForm"
        >
          Cancel Todo
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import todoFormTitle from "./todoForm_components/todoFormTitle.vue";
  export default {
  components: {
    todoFormTitle,
},
  props: {
    isFormOpen: {
      type: Boolean,
      default: false
    },
    isEdit: {
      type: Boolean,
      // default: false
    },
    todoArray: {
      type: Array,
    },
    // todoObjectToEdit: {
    //   type: Object,
    // //   // default: {
    // //   //   title,
    // //   //   selectedStatus,
    // //   //   dateAdded
    // //   // }
    // }
  },

  data() {
    return {
      title: "",
      status: "",
      dateAdded: "",

      todo: {
        title: "",
        selectedStatus: "",
        dateAdded: ""
      },
    }
  },
  methods: {
    resetModelValue: function(){
      this.todo = {
        title: "",
        selectedStatus: "",
        dateAdded: ""
      }
    },
    onSubmitForm: function(event){

      let dateToString;
      const currentTimeMillis = new Date();
      dateToString = currentTimeMillis.toDateString() + " " + currentTimeMillis.toLocaleTimeString(); //.slice(4, 15) //09:37:53
      this.dateAdded = dateToString.toString();
      this.todo.title = this.title;
      this.todo.selectedStatus = this.status;
      this.todo.dateAdded = this.dateAdded;
      this.title = "";this.status = ""; this.dateAdded = "";
        this.$emit("todoObject", this.todo)

      event.target.reset(); 
      this.resetModelValue()
    },
    handleCloseForm(){
      this.$emit("handleCloseForm")
    }
  },
  emits: ["todoObject", "handleCloseForm"],
  // computed: {
  //   setTitleModel(){
  //     if(!this.$props.isEdit){
  //       return this.modelValueEdit
  //     } else {
  //       return this.modelValueAdd
  //     }
  //   }
  // }
};
</script>

<style scoped>
.form-wrapper {
  width: 100%;
  height: 100vh;
  background-color: var(--colorNotWhite);
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  /* display: none; */
}
.form-container {
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 0.25rem;
  padding: 1rem;
  background-color: var(--colorCloseWhite);
  border-radius: 0.375rem;
}
.todo-input-label {
  margin-top: 1rem;
}
.todo-input-label, .todo-select-label {
  font-size: 1rem;
  font-weight: 400;
}
.todo-input, .todo-select {
  font-size: 0.875rem;
  font-weight: 300;
  padding: 0.375rem;
  margin-bottom: 0.875rem;
  border-radius: 0.25rem;
  background-color: #dbdbdb;
  border: 1px solid #E1E1E1;
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
.todo-form-btn-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: .5rem;
  margin-bottom: 1rem;
}
.todo-form-btn {
  width: 100%;
  display: flex;
  text-align: center;
  justify-content: center;
  padding: 0.5rem;
  font-size: 0.875rem;
  font-weight: 300;
  border: none;
  box-shadow: 10px 10px 20px 20px #181818,;
  color: #F1F1F1;
  border-radius: 0.25rem;
  margin-top: .25rem;
  /* outline: none; */
}
.btn-primary {
  background: #005BD3;
}
.btn-primary:hover {
  background: #858585;
  color:#181818;
}
.btn-primary:focus {
  background: #858585;
  color:#181818;
  outline: 2px solid #005BD3;

}
.btn-secondary {
  background: #858585;
}
.btn-secondary:hover {
  background: #858585;
}
.btn-secondary:focus {
  background: #858585;
  outline: 2px solid #005BD3;
}

</style>
