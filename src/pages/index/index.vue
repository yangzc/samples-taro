<template>
  <view class="index">
    <!-- <Counter /> -->
    <float-menu :distance="200" ref="floatMenu">
      <template #float-menu>
        <view
          @tap="menuTap"
          style="
            background-color: blue;
            width: 150rpx;
            height: 150rpx;
            border-radius: 50%;
            text-align: center;
            line-height: 150rpx;
          "
          >Button</view
        >
      </template>
      <template #menu-list-item="{ index }">
        <view
          @tap="itemTap"
          style="
            background-color: red;
            width: 80rpx;
            height: 80rpx;
            border-radius: 50%;
            text-align: center;
            line-height: 80rpx;
          "
          >{{ index }}</view
        >
      </template>
    </float-menu>
  </view>
</template>

<script setup>
import "./index.scss";
import FloatMenu from "@/components/FloatMenu.vue";
import { ref } from "vue";
defineOptions({
  name: "IndexPage",
});
const floatMenu = ref();

const menuTap = () => {
  floatMenu.value.openOrClose();
};

const itemTap = () => {
  console.log("itemTap...");
};
</script>
