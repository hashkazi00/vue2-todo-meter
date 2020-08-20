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
      <DoLater
        :doLater="doLater"
        @deleteTodoLater="deleteTodoLater"
        @doneLater="doneLater"
        @resumeLater="resumeLater"
      />
      <Completed :completed="completed" @deleteTodoFinal="deleteTodoFinal" @redoFinal="redoFinal" />
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
      completed: [],
      STORAGE_KEY1: "latestAdded",
      STORAGE_KEY2: "doLater",
      STORAGE_KEY3: "completed"
    };
  },
  created() {
    this.latestAdded = JSON.parse(
      localStorage.getItem(this.STORAGE_KEY1) || "[]"
    );
    this.doLater = JSON.parse(localStorage.getItem(this.STORAGE_KEY2) || "[]");
    this.completed = JSON.parse(
      localStorage.getItem(this.STORAGE_KEY3) || "[]"
    );
  },
  methods: {
    addTodoItem(value) {
      this.latestAdded.push({
        id: uuid.v4(),
        title: value,
        status: "pending"
      });
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.latestAdded));
      this.keepListShort();
    },
    laterTodo(index) {
      this.doLater.push(this.latestAdded[index]);
      localStorage.setItem(this.STORAGE_KEY2, JSON.stringify(this.doLater));
      this.$delete(this.latestAdded, index);
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.latestAdded));
    },
    done(index) {
      this.completed.push(this.latestAdded[index]);
      localStorage.setItem(this.STORAGE_KEY3, JSON.stringify(this.completed));
      this.$delete(this.latestAdded, index);
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.latestAdded));
    },
    doneLater(index) {
      this.completed.push(this.doLater[index]);
      localStorage.setItem(this.STORAGE_KEY3, JSON.stringify(this.completed));
      this.$delete(this.doLater, index);
      localStorage.setItem(this.STORAGE_KEY2, JSON.stringify(this.doLater));
    },
    resumeLater(index) {
      this.latestAdded.push(this.doLater[index]);
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.latestAdded));
      this.$delete(this.doLater, index);
      localStorage.setItem(this.STORAGE_KEY2, JSON.stringify(this.doLater));
    },
    deleteTodoItem(index) {
      this.$delete(this.latestAdded, index);
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.completed));
    },
    deleteTodoLater(index) {
      this.$delete(this.doLater, index);
      localStorage.setItem(this.STORAGE_KEY2, JSON.stringify(this.doLater));
    },
    deleteTodoFinal(index) {
      this.$delete(this.completed, index);
      localStorage.setItem(this.STORAGE_KEY3, JSON.stringify(this.completed));
    },
    redoFinal(index) {
      this.latestAdded.push(this.completed[index]);
      localStorage.setItem(this.STORAGE_KEY1, JSON.stringify(this.latestAdded));
      this.$delete(this.completed, index);
      localStorage.setItem(this.STORAGE_KEY3, JSON.stringify(this.completed));
    },
    keepListShort() {
      for (var key in window.localStorage) {
        // eslint-disable-next-line no-prototype-builtins
        if (window.localStorage.hasOwnProperty(key)) {
          this.data += window.localStorage[key];
          if (
            ((window.localStorage[key].length * 16) / (8 * 1024)).toFixed(2) >=
            5
          ) {
            alert(
              "You have exceeded the localStorage, please delete a few completed items or reset to use the app again"
            );
          }
        }
      }
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

@media only screen and (max-width: 450px) {
  .container {
    min-width: 40rem;
  }
}
@media only screen and (max-width: 350px) {
  .container {
    min-width: 32rem;
  }
}
</style>
