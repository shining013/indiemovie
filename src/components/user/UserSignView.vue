<template>
  <div>
    <form></form>
    <div class="mb-1">
      <input
        type="text"
        class="form-control"
        placeholder="userId"
        v-model="userdata.userId"
      />
    </div>
    <div class="mb-1">
      <input
        type="text"
        class="form-control"
        placeholder="password"
        v-model="userdata.password"
      />
    </div>
    <div class="mb-1">
      <input
        type="text"
        class="form-control"
        placeholder="username"
        v-model="userdata.username"
      />
    </div>
    <div class="input-group mb-3">
      <input
        type="file"
        class="form-control"
        id="fileform"
        @change="handleImage"
        accept="image/*"
      />

      <label class="input-group-text" for="fileform">Upload</label>
    </div>
    <div class="mb-1">
      <input
        type="text"
        class="form-control"
        placeholder="my-theater"
        v-model="userdata.theater"
      />
    </div>

    <div class="btn" style="background-color: fuchsia" @click="addUser">
      submit
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useStore } from "vuex";

const store = useStore();
const userdata = ref({
  userId: null,
  password: null,
  username: null,
  addr: null,
  image: null,
  theater: null,
});

const clearform = () => {
  userdata.value.userId = null;
  userdata.value.password = null;
  userdata.value.username = null;
  userdata.value.addr = null;
  userdata.value.image = null;
  userdata.value.theater = null;
};

const addUser = () => {
  let uData = {
    userId: userdata.value.userId,
    password: userdata.value.password,
    username: userdata.value.username,
    addr: userdata.value.addr,
    image: userdata.value.image,
    theater: userdata.value.theater,
  };
  store.commit("addUser", uData);
  clearform();
};

const handleImage = (e) => {
  const file = e.target.files[0];
  console.log(file);
  if (file) {
    userdata.value.image = URL.createObjectURL(file);
  }
};
</script>

<style lang="scss" scoped>
.btn {
  height: 50px;
}
</style>
