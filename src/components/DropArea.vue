<script>
import FileSlider from "@/components/FileSlider.vue";

import uploadFiles from "@/utils/uploadFiles";

import IcUpload from "@/assets/icons/IcUpload.vue";
import { formatFileSize } from '@/utils/format';

export default {
  props: {
    maxFile: Number,
    maxSize: Number,
  },
  components: {
    FileSlider,
    IcUpload,
  },
  data() {
    return {
      listFilesChosen: [],
      isError: false,
      errorMessage: "",
    };
  },
  methods: {
    handleDragOver() {
      event.preventDefault();
    },
    handleDropFile() {
      event.preventDefault();
      this.validateFileSize(event.dataTransfer.files[0]);
    },
    handleChoseFile() {
      this.validateFileSize(event.target.files[0]);
    },
    handleUpload() {
      uploadFiles(this.listFilesChosen).then(() => {
        console.log("upload done");
        this.listFilesChosen.splice(0, this.listFilesChosen.length);
      });
    },
    checkSize(file, size) {
      return file.size <= size;
    },
    validateFileSize(file) {
      console.log(file.size, this.maxSize);
      if (this.checkSize(file, this.maxSize)) {
        this.listFilesChosen.push(file);
        this.isError = false;
      } else {
        this.errorMessage = "The maximum file size is " + formatFileSize(this.maxSize);
        this.isError = true;
      }
    },
  },
  watch: {
    listFilesChosen() {
      if (this.listFilesChosen.length > this.maxFile) {
        this.isError = true;
        this.errorMessage = "The maximum number of files is " + this.maxFile;
        this.listFilesChosen.pop();
      }
    },
    isError() {
      if(!this.isError) {
        this.errorMessage = ''
      }
    }
  },
};
</script>

<template>
  <div class="main-area">
    <div class="main-container-wrapper">
      <div
        :class="['main-container', isError ? 'error' : '']"
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
      <p class="error-message" v-if="errorMessage">
        {{ errorMessage }}
      </p>
    </div>
    <file-slider :listFile="listFilesChosen" />
    <button class="upload-btn" @click="handleUpload">Upload</button>
  </div>
</template>

<style lang="scss" scoped>
@import "@/styles/DropArea.scss";
</style>