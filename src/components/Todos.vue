<template>
  <div style="text-align: center;">
    <h3>Todos</h3>
          <span >click to mark as complete</span>

    <hr />
    <div class="legend">
      
      
    
    </div>
     
    <div class="todos">
      
      <div
        @click="onClick(todo)"
        v-for="todo in allTodos"
        :key="todo.id"
        class="todo"
        v-bind:class="{'is-complete':todo.completed}"
      >
     
        {{ todo.title }}
        <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Todos",
  methods: {
    ...mapActions(["getTodos", "deleteTodo", "updateTodo"]),
    onClick(todo) {
      const updTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed
      };

      this.updateTodo(updTodo);
    }
  },
  computed: mapGetters(["allTodos"]),
  created() {
    this.getTodos();
  }
};
</script>

<style scoped>
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

.todo {
  border: 1px solid #ccc;
  background: #1c794f;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
  width: 60%;
  transition: 250ms;
  height: 60%;
}

.todo:hover {
margin-top: 2px ;
box-shadow: 7px 4px 5px 0px rgba(0,0,0,0.4);

}

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #fff;
  cursor: pointer;
}

.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #35495e;
}

.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41b883;
}

.is-complete {
  background: #833636;
  color: #fff;
}


</style>
