<template>
  <div v-if="$store.state.userData.length" class="scrollable-container">
    <div
      v-for="(item, i) in $store.state.userData"
      :key="i"
      class="d-flex gap-2 border rounded p-3 mb-3 scroll-item"
    >
      <div class="avata">
        <img :src="item.image" alt="" />
      </div>
      <div>
        <h5 class="mb-0">{{ item.userid }}</h5>
        <p class="mb-0">{{ item.username }}</p>
        <p class="mb-0">{{ item.theater }}</p>
        <div @click="deleteUser(i)">❌</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useStore } from "vuex";
const store = useStore();
const deleteUser = (index) => {
  alert("정말 삭제하시겠습니까?");
  store.commit("deleteUser", index);
};
</script>

<style lang="scss" scoped>
.avata {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
}

.btn,
.btn-primay {
  width: 15px;
  height: 15px;
}

.scrollable-container {
  height: 300px;
  overflow-y: auto;
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
