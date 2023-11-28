<script>
import FileSlider from "@/components/FileSlider.vue";

import uploadFiles from "@/utils/uploadFiles";

import IcUpload from "@/assets/icons/IcUpload.vue";

export default {
  components: {
    FileSlider,
    IcUpload,
  },
  data() {
    return {
      listFilesChosen: [],
    };
  },
  methods: {
    handleDragOver() {
      event.preventDefault();
    },
    handleDropFile() {
      event.preventDefault();
      this.listFilesChosen.push(event.dataTransfer.files[0]);
    },
    handleChoseFile() {
      this.listFilesChosen.push(event.target.files[0]);
    },
    handleUpload() {
      uploadFiles(this.listFilesChosen).then(() => {
        console.log('upload done');
        this.listFilesChosen.splice(0, this.listFilesChosen.length)
      });
    },
  },
};
</script>

<template>
  <div class="main-area">
    <div
      class="main-container"
      @dragover="handleDragOver"
      @drop="handleDropFile"
    >
      <div class="drop-area">
        <div class="content">
          <ic-upload></ic-upload>
          <div class="text">
            <p class="desc">Drag and drop files</p>
            <label for="file-uploader" class="label-uploader"
              >Browse files</label
            >
            <input
              type="file"
              id="file-uploader"
              hidden
              @change="handleChoseFile"
            />
          </div>
        </div>
      </div>
    </div>
    <file-slider :listFile="listFilesChosen" />
    <button class="upload-btn" @click="handleUpload">Upload</button>
  </div>
</template>

<style lang="scss" scoped>
@import "@/styles/DropArea.scss";
</style>