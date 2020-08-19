<template>
  <div class="container__progress">
    <div class="circle latest-added">
      <p>{{latestAdded.length}}</p>
    </div>
    <div class="circle do-later">
      <p>{{doLater.length}}</p>
    </div>
    <div class="circle completed">
      <p>{{completed.length}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Meter",
  props: ["latestAdded", "doLater", "completed"]
};
</script>

<style scoped>
.container__progress {
  display: flex;
  justify-content: space-around;
  font-size: 1.8rem;
}
.circle {
  height: 6rem;
  width: 6rem;
  border-radius: 50%;
  /* background-color: bisque; */
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid black;
  color: white;
}
.latest-added {
  background-color: #91d18b;
}
.do-later {
  background-color: #ffaa71;
}
.completed {
  background-color: #cf1b1b;
}
</style>