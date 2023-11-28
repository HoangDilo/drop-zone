<script>
import { formatFileSize } from "@/utils/format";

import CustomFileTag from "./CustomFileTag.vue";

import IcLeftArrow from "@/assets/icons/IcLeftArrow.vue";
import IcRightArrow from "@/assets/icons/IcRightArrow.vue";

export default {
  components: {
    IcRightArrow,
    IcLeftArrow,
  },
  props: {
    listFile: {
      type: Array,
      default: [],
    },
  },
  components: { CustomFileTag, IcLeftArrow, IcRightArrow },
  methods: {
    handleRemoveFile(index) {
      this.listFile.splice(index, 1);
    },
    formatFileSize,
    handleGoLeft() {
      this.$refs["slider-container"].scrollLeft -= 140;
    },
    handleGoRight() {
      this.$refs["slider-container"].scrollLeft += 140;
    },
  },
};
</script>

<template>
  <div class="slider-button-container">
    <div class="arrows" @click="handleGoLeft">
      <IcLeftArrow />
    </div>
    <div class="slider-container" ref="slider-container">
      <div class="file-tags">
        <CustomFileTag
          v-for="(item, index) in listFile"
          :fileIndex="index"
          :fileType="item.type"
          :key="index"
          @remove-file="(index) => handleRemoveFile(index)"
        >
          <div class="info-container">
            <span class="file-name">{{ item.name }}</span>
            <span class="file-size">{{ formatFileSize(item.size) }}</span>
          </div>
        </CustomFileTag>
      </div>
    </div>
    <div class="arrows" @click="handleGoRight">
      <IcRightArrow />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "@/styles/DropArea.scss";
</style>