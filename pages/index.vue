<template>
  <!-- <div class="complete">
    <div class="play-form-box">
      <img src="/img/1.jpg" alt="播放器轮盘" />
    </div>
    <div class="play-line-box"></div>
  </div> -->
  <div class="complete">
    <div class="play-from-box">
      <div
        v-for="(item, index) in splitLineData"
        :key="`play-form-${index}`"
        :ref="setSplitLineRef"
        class="play-bar-box"
      ></div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  setup() {
    const splitLineData = ref([]);
    const splitLineRefs = ref([]);
    for (let i = 0; i < 100; i++) {
      splitLineData.value.push(Math.random(10));
    }
    const setSplitLineRef = (el) => {
      splitLineRefs.value.push(el);
    };
    return {
      splitLineRefs,
      splitLineData,
      setSplitLineRef,
    };
  },
  mounted() {
    console.log("mounted执行了");
    nextTick(() => {
      this.splitLineRefs.forEach((splitLineRef, index) => {
        if (!splitLineRef) {
          return;
        }
        splitLineRef.style.left = `${index}em`;
        splitLineRef.style.height = `${Math.random(10) * 2}em`;
      });
    });
  },
});
</script>


<style lang="scss" scoped>
.complete {
  height: 100vh;
  width: 100vw;
  background: linear-gradient(to top right, #5433ff, #20bdff, #a5fecb);
  position: relative;
  .split-line-box {
    position: absolute;
    top: 80%;
    width: calc(100% - 0.1em);
    height: 0em;
    border-bottom: 0.1em blue solid;
  }
  .play-from-box {
    position: absolute;
    top: 80%;
    display: flex;
    align-items: flex-end;
    width: 100%;
    border-bottom: 0.1em blue solid;
  }
  .play-bar-box {
    width: 0.8em;
    background: red;
    top: calc(80% - 1em);
    height: 1em;
    margin-left: 0.1em;
  }
}
</style>