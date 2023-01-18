<template>
  <div class="box-wrapper">
    <div class="block" v-if="showBlock" @click="stopTimer()">
      <p></p>
    </div>
  </div>
</template>

<script setup>
import { defineEmits, ref, onMounted, onUpdated, onUnmounted } from "vue";

const props = defineProps(["delay"]);
const emit = defineEmits(["end"]);

let showBlock = ref(false);
let timer = ref(null);
let reactionTime = ref(0);

onMounted(() => {
  setTimeout(() => {
    showBlock.value = true;

    startTimer();
  }, props.delay);
});

const startTimer = () => {
  timer.value = setInterval(() => {
    console.log(reactionTime.value);
    reactionTime.value += 10;
  }, 10);
};

const stopTimer = () => {
  clearInterval(timer.value);
  emit("end", reactionTime.value);
};

onUpdated(() => {
  if (showBlock.value) {
    const box = document.querySelector(".block");

    var fullWidth = window.innerWidth - 10;
    var fullHeight = window.innerHeight - 10;

    box.style.position = "absolute";
    box.style.left = Math.round(Math.random() * fullWidth) + "px";
    box.style.top = Math.round(Math.random() * fullHeight) + "px";

    box.style.borderRadius = Math.random() * 100 + "%";

    box.style.backgroundColor = `rgb(${Math.random() * 255}, ${
      Math.random() * 255
    }, ${Math.random() * 255})`;

    box.style.width = Math.random() * 30 + "%";
    box.style.height = Math.random() * 30 + "%";
  }
});

onUnmounted(() => {
  console.log("unmounted");
});
</script>
<style lang="scss" scoped>
.box-wrapper {
  max-width: 100%;
  max-height: 100%;
  min-height: 100%;
  min-width: 100%;
}
.block {
  border: 2px solid lime;
  text-align: center;
}
</style>
