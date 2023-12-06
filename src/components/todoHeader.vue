<template>
  <nav>
    <todoHeaderStructure>
      <template #headerTitle>
        <h1 aria-label="Todo list navigation title" class="headerTitleItem">
          Todo List App
        </h1>
      </template>
      <template #headerTimer>
        <h3
          aria-label="Todo list navigation item for today's date"
          class="headerTimeItem"
        >
          {{ `${todayDate}` }}
        </h3>
        <h3
          aria-label="Todo list navigation item for current time"
          class="headerTimeItem"
        >
          {{ `${todayTime}` }}
        </h3>
      </template>
    </todoHeaderStructure>
  </nav>
  <TodoForm :todayDate="todayTime" />
</template>

<script>
import TodoForm from "./todoForm.vue";
import todoHeaderStructure from "./todoHeader_components/todoHeader_Structure.vue";
export default {
  components: {
    todoHeaderStructure,
    TodoForm,
  },
  data() {
    return {
      todayTime: "",
      todayDate: "",
    };
  },
  methods: {
    getTimeToday: function () {
      const currentTimeMillis = new Date();
      this.todayDate = currentTimeMillis.toDateString(); //.slice(4, 15) //09:37:53
      this.todayTime = currentTimeMillis.toLocaleTimeString(); //09:37:53
    },
  },
  created() {
    setInterval(() => {
      this.getTimeToday();
    }, 1000);
  },
};
</script>

<style scoped>
.headerTitleItem {
  display: flex;
  text-align: start;
  justify-content: flex-start;
  font-size: 2rem;
  font-weight: 600;
  padding: 0.25rem;
}
.headerTimeItem {
  display: flex;
  text-align: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: 300;
  padding: 0.75rem;
}
.headerTimeItem,
.headerTitleItem {
  color: var(--ColorOffWhite);
}
</style>
