
<script>
import IcClose from "@/assets/icons/IcClose.vue";
import IcExcelFile from "@/assets/icons/IcExcelFile.vue";
import IcPdfFile from "@/assets/icons/IcPdfFile.vue";
import IcWordFile from "@/assets/icons/IcWordFile.vue";
import IcOtherFiles from "@/assets/icons/IcOtherFiles.vue";

export default {
  components: {
    IcClose,
    IcExcelFile,
    IcPdfFile,
    IcWordFile,
    IcOtherFiles,
  },
  props: {
    fileType: String,
    fileIndex: Number,
  },
  methods: {
    configType() {
      switch (this.fileType) {
        case "application/pdf":
          return IcPdfFile;
        case "application/vnd.openxmlformats-officedocument.wordprocessingml.document":
          return IcWordFile;
        case "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet":
          return IcExcelFile;
        default:
          return IcOtherFiles;
      }
    },
    handleRemove() {
      this.$emit("remove-file", this.fileIndex);
    },
  },
};
</script>

<template>
  <div class="file-tag">
    <div class="file-info">
      <div class="file-icon-wrapper">
        <component :is="configType()"></component>
      </div>
      <slot></slot>
    </div>
    <div @click="handleRemove">
      <ic-close />
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "@/styles/DropArea.scss";
</style>