<template>
  <div id="app">
    <div class="container">
      <Header />
      <Meter :latestAdded="latestAdded" :doLater="doLater" :completed="completed" />
      <AddTodo @addTodo="addTodoItem" />
      <OnGoing
        :latestAdded="latestAdded"
        @deleteTodo="deleteTodoItem"
        @later="laterTodo"
        @done="done"
      />
      <DoLater :doLater="doLater" @deleteTodoLater="deleteTodoLater" @doneLater="doneLater" />
      <Completed :completed="completed" @deleteTodoFinal="deleteTodoFinal" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import Meter from "./components/Meter";
import AddTodo from "./components/AddTodo";
import OnGoing from "./components/OnGoing";
import DoLater from "./components/DoLater";
import Completed from "./components/Completed";

import { uuid } from "vue-uuid";

export default {
  name: "App",
  components: {
    Header,
    Meter,
    AddTodo,
    OnGoing,
    DoLater,
    Completed
  },
  data() {
    return {
      latestAdded: [],
      doLater: [],
      completed: []
    };
  },
  methods: {
    addTodoItem(value) {
      this.latestAdded.push({
        id: uuid.v4(),
        title: value,
        status: "pending"
      });
    },
    laterTodo(index) {
      this.doLater.push(this.latestAdded[index]);
      this.$delete(this.latestAdded, index);
    },
    done(index) {
      this.completed.push(this.latestAdded[index]);
      this.$delete(this.latestAdded, index);
    },
    doneLater(index) {
      this.completed.push(this.doLater[index]);
      this.$delete(this.doLater, index);
    },
    deleteTodoItem(index) {
      this.$delete(this.latestAdded, index);
    },
    deleteTodoLater(index) {
      this.$delete(this.doLater, index);
    },
    deleteTodoFinal(index) {
      this.$delete(this.completed, index);
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Poppins:400,600,700&display=swap");
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  -webkit-box-sizing: inherit;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
}

body {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
  background-color: #131516;
  position: relative;
  height: 100vh;
}

.container {
  position: absolute;
  top: 10%;
  left: 50%;
  -webkit-transform: translate(-50%);
  transform: translate(-50%);
  min-width: 40rem;
  /* height: 50%; */
  background-color: #f8b0b4;
  padding: 0 1rem 0 1rem;
  border-radius: 5px;
}
@media only screen and (max-width: 800px) {
  html {
    font-size: 52.5%;
  }
}

@media only screen and (max-width: 550px) {
  .container {
    min-width: 36rem;
  }
}

@media only screen and (max-width: 450px) {
  .container {
    min-width: 32rem;
  }
}
</style>
