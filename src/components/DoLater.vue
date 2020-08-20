<template>
  <div>
    <div @click="isVisible = !isVisible" class="container__subHeading">
      <svg
        v-if="!isVisible"
        version="1.1"
        width="20"
        height="20"
        id="Capa_1"
        x="0px"
        y="0px"
        viewBox="0 0 256 256"
        style="enable-background:new 0 0 256 256;"
        xml:space="preserve"
      >
        <g>
          <g>
            <polygon
              points="79.093,0 48.907,30.187 146.72,128 48.907,225.813 79.093,256 207.093,128 		"
            />
          </g>
        </g>
      </svg>
      <svg
        v-if="isVisible"
        version="1.1"
        id="Capa_1"
        x="0px"
        y="0px"
        width="20"
        height="20"
        viewBox="0 0 306 306"
        style="enable-background:new 0 0 306 306;"
        xml:space="preserve"
      >
        <g>
          <g id="expand-more">
            <polygon points="270.3,58.65 153,175.95 35.7,58.65 0,94.35 153,247.35 306,94.35 		" />
          </g>
        </g>
      </svg>
      <h2>Do Later</h2>
    </div>
    <div v-if="isVisible">
      <div v-for="(item, index) in doLater" :key="index">
        <div class="container__todoItem">
          <h2>{{item.title}}</h2>
          <div class="container__todoItem--actions">
            <svg
              @click="deleteTodo(index)"
              class="close"
              version="1.1"
              viewBox="0 0 357 357"
              style="enable-background:new 0 0 357 357;"
              xml:space="preserve"
            >
              <g>
                <g id="close">
                  <polygon
                    points="357,35.7 321.3,0 178.5,142.8 35.7,0 0,35.7 142.8,178.5 0,321.3 35.7,357 178.5,214.2 321.3,357 357,321.3
                   214.2,178.5"
                  />
                </g>
              </g>
            </svg>
            <svg
              @click="resume(index)"
              class="resume"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
            >
              <path d="M3 22v-20l18 10-18 10z" />
            </svg>
            <svg
              @click="done(index)"
              class="done"
              version="1.1"
              id="Capa_1"
              x="0px"
              y="0px"
              viewBox="0 0 375.147 375.147"
              style="enable-background:new 0 0 375.147 375.147;"
              xml:space="preserve"
            >
              <g>
                <g>
                  <polygon
                    points="344.96,44.48 119.147,270.293 30.187,181.333 0,211.52 119.147,330.667 375.147,74.667 		"
                  />
                </g>
              </g>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DoLater",
  data() {
    return { isVisible: false };
  },
  methods: {
    deleteTodo(index) {
      this.$emit("deleteTodoLater", index);
    },
    resume(index) {
      this.$emit("resumeLater", index);
    },
    done(index) {
      this.$emit("doneLater", index);
    }
  },
  props: ["doLater"]
};
</script>

<style scoped>
.container__todoItem {
  margin-top: 10px;
  margin-bottom: 1rem;
  height: 6rem;
  background-color: #1f2124;
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

.container__todoItem h2 {
  padding-left: 20px;
  font-size: 1.8rem;
  caret-color: #fff;
  color: #fff;
  letter-spacing: 0.5px;
  font-weight: 400;
}

.container__todoItem--actions {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  margin-right: 20px;
}

.container__todoItem--actions svg {
  width: 1.8rem;
  height: 1.8rem;
  cursor: pointer;
  opacity: 0.5;
  -webkit-transition: all 0.2s linear;
  transition: all 0.2s linear;
  margin-left: 1.8rem;
  opacity: 1;
}

.container__todoItem--actions svg:first-child {
  margin-left: 0;
}

.close {
  fill: #ff1a55;
}

.pause {
  fill: #ffc935;
}

.done {
  fill: #2fde49;
}
.resume {
  fill: #ffc935;
}

.container__subHeading {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  font-size: 1.5rem;
  margin-top: 1rem;
  margin-bottom: 1rem;
  opacity: 0.6;
  cursor: pointer;
}

.container__subHeading:hover {
  opacity: 0.8;
}

.container__subHeading svg {
  fill: #fff;
}

.container__subHeading h2 {
  margin-left: 10px;
}

.container__subHeading h2 span {
  font-size: 1.5rem;
}
</style>