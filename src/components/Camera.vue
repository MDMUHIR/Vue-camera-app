<template>
  <div
    class="container-sm d-flex justify-content-center align-items-center flex-column"
    style="background-color: #34495e;"
  >
    <div class=" text-center position-relative justify-content-center align-items-center flex-column" style="width: 85%;">
      <video
        src=""
        ref="video"
        autoplay
        playsinline=""
        webkit-playsinline
        muted
        hidden
      ></video>
      <canvas
        ref="canvas"
        width="1080"
        height="720"
        class="bg-dark rounded w-75 shadow-lg border"
      ></canvas>
      <button @click="takePicture" class="btn btn-light rounded-circle  position-absolute top-100 start-50 translate-middle border-3 border-light  " style="width: 60px;
      height: 60px; border-bottom: 2px solid black !important; ">Cap</button>
    </div>
   
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const video = ref(null);
const canvas = ref(null);
const ctx = ref(null);

const constraints = ref({
  audio: false,
  video: true,
});

onMounted(async () => {
  if (video.value && canvas.value) {
    ctx.value = canvas.value.getContext("2d");

    await navigator.mediaDevices
      .getUserMedia(constraints.value)
      .then(setStream)
      .catch((e) => {
        console.error(e);
      });
  }
});
const setStream = (stream) => {
  video.value.srcObject = stream;
  video.value.play();
  requestAnimationFrame(Draw);
};

const Draw = () => {
  ctx.value.drawImage(
    video.value,
    0,
    0,
    canvas.value.width,
    canvas.value.height
  );
  requestAnimationFrame(Draw);
};

// To download the context......
const takePicture = () => {
  let link = document.createElement("a");
  link.download = `vue-cam-${new Date().toISOString()}.png`;
  link.href = canvas.value.toDataURL();
  link.click();
};
</script>