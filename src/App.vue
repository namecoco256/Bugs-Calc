<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { bugs } from './bugs.js'
import { ref, computed } from 'vue'

const total = ref(0);

const sortKey = ref('sell'); // デフォルトソートキー
const sortAsc = ref(false);  // デフォルトは昇順

// ソートされたリストを計算
const sortedBugs = computed(() => {
  return [...bugs].sort((a, b) => {
    const sortOrder = sortAsc.value ? 1 : -1;
    if (a[sortKey.value] > b[sortKey.value]) return sortOrder;
    if (a[sortKey.value] < b[sortKey.value]) return -sortOrder;
    return 0;
  });
});
</script>

<template>
  <div class="total">
    <h2>合計 {{ total.toLocaleString() }}ベル だなも！</h2>
  </div>
  <div class="sort">
    <button @click="sortKey = 'sell'">価格順</button>
    <button @click="sortKey = 'name'">名前順</button> <br>
    <button @click="sortAsc = !sortAsc">昇順-降順</button>

  </div>
  <button v-for="bug in sortedBugs" :key="bug.name" class="bug" @click="total += bug.sell">
    <img :src="bug.img" alt="" />
    <pre>{{ bug.name + "　".repeat(8-bug.name.length)}} : {{ bug.sell }}ベル{{ " ".repeat(5-bug.sell.toString().length)}}</pre>
  </button>
</template>

<style scoped>
.bug{
  display: flex;
  background-color: #1a1a1a;
  margin: 10px;
  padding: 10px;
  border-radius: 10px;
  color: white;
  font-size: 20px;
  text-align: center;
}
.bug > * {
  margin-left: 0.5em;
  margin-right: 0.5em;
}
</style>
