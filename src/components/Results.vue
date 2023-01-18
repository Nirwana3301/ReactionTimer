<template>
  <div class="score-box">{{ props.score }}</div>
  <div class="rank-box">{{ rank }}</div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps(['score']);

let rank = ref('');

onMounted(() => {
  if (props.score < 200) {
    rank.value = 'Master';
  } else if (props.score < 400) {
    rank.value = 'Expert';
  } else if (props.score < 600) {
    rank.value = 'Average';
  } else {
    rank.value = 'Beginner';
  }
});

</script>

<style lang="scss" scoped>
.score-box {
  font-size: 2rem;
  font-weight: bold;
  color: #fff;
  text-align: center;
}

.rank-box {
  font-size: 2rem;
  font-weight: bold;
  color: #fff;
  text-align: center;
}
</style>
