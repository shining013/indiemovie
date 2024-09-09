<template>
  <div>
    <form></form>
    <div class="mb-2">
      <input
        type="text"
        class="form-control"
        placeholder="name"
        v-model="movieData.content"
      />
    </div>
    <div class="mb-2">
      <input
        type="text"
        class="form-control"
        placeholder="address"
        v-model="movieData.address"
      />
    </div>
    <div class="mb-2">
      <input
        type="text"
        class="form-control"
        placeholder="detail"
        v-model="movieData.detail"
      />
    </div>
    <div class="btn" style="background-color: fuchsia" @click="addTheater">
      add
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useStore } from "vuex";

const store = useStore();
const movieData = ref({
  content: null,
  address: null,
});

const clearform = () => {
  movieData.value.content = null;
  movieData.value.address = null;
};

const addTheater = () => {
  let mData = {
    content: movieData.value.content,
    address: movieData.value.address,
  };
  store.commit("addTheater", mData);
  clearform();
};
</script>

<style lang="scss" scoped></style>
