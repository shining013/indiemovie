<template>
  <div class="container py-2">
    <div class="row">
      <div class="row col-md-3 col-sm-3">
        <div class="">
          <PositionListView />
        </div>
      </div>
      <div class="row col-md-3">
        <div class="">
          <h3>theater add</h3>
          <PositionAddView />
        </div>
      </div>
      <div class="col-md-3 col-sm-3">
        <h3>User List</h3>
        <UserListView />
      </div>
      <div class="col-md-3 col-sm-3">
        <h3>User sign</h3>
        <UserSignView />
      </div>
      <div class="row">
        <div class="col-md-5 mb-3 col-sm-6">
          <MapView />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import UserListView from "../components/user/UserListView.vue";
import UserSignView from "../components/user/UserSignView.vue";
import MapView from "../components/user/MappingView.vue";
import RestView from "../components/user/RestView.vue";
import PositionListView from "../components/user/PositionListView.vue";
import PositionAddView from "../components/user/PositionAddView.vue";
</script>

<style lang="scss" scoped></style>
