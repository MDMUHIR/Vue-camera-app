<template>
  <div
    class="w-100 vh-100 d-flex justify-content-center align-items-center flex-column"
    style="background-color: #34495e"
  >
    <Camera />
    <a
      class="creator position-fixed bottom-0 end-0 btn btn-light p-0 ps-1 pe-1 rounded-start-2 rounded-end-0 fw-light text-decoration-none fst-italic text-dark"
      href="https://github.com/MDMUHIR"
      >© MDMUHIR</a
    >
  </div>
</template>

<script setup>
import Camera from "./components/Camera.vue";
</script>
