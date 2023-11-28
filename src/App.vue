<script>
import DropArea from "./components/DropArea.vue";

export default {
  components: {
    DropArea,
  }
};
</script>

<template>
  <div class="main-screen">
    <drop-area />
  </div>
</template>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.main-screen {
  height: 600px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>