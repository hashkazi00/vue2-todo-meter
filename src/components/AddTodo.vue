<template>
  <div class="container__addTodo">
    <input
      v-model="todo"
      type="text"
      placeholder="What needs to be done?"
      v-on:keyup.enter="addTodo()"
    />
    <svg
      @click="addTodo()"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      width="40"
      height="40"
    >
      <path
        class="heroicon-ui"
        d="M17 11a1 1 0 0 1 0 2h-4v4a1 1 0 0 1-2 0v-4H7a1 1 0 0 1 0-2h4V7a1 1 0 0 1 2 0v4h4z"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      todo: ""
    };
  },
  methods: {
    addTodo() {
      if (this.todo !== "") {
        this.$emit("addTodo", this.todo);
        this.todo = "";
      }
    }
  }
};
</script>

 <style scoped>
.container__addTodo {
  margin-top: 2rem;
  margin-bottom: 1rem;
  height: 6rem;
  background-color: #0d0e0f;
  width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  border-radius: 5px;
}

.container__addTodo input {
  height: 100%;
  width: 100%;
  background: none;
  border: none;
  padding-left: 20px;
  font-size: 1.8rem;
  outline: none;
  caret-color: #fff;
  color: #fff;
}

.container__addTodo svg {
  fill: #fff;
  margin-right: 10px;
  cursor: pointer;
  opacity: 0.5;
  -webkit-transition: all 0.2s linear;
  transition: all 0.2s linear;
}

.container__addTodo svg:hover {
  opacity: 1;
}
</style>