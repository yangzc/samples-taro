<template>
  <view class="index">
    <!-- <Counter /> -->
    <float-menu :distance="200" ref="floatMenu" :menuCount="menuItems.length">
      <template #float-menu>
        <view class="float-menu" @tap="menuTap">
          <image
            class="float-menu-bg"
            src="https://susuanqiniu.knowbox.cn/fe/wx-shop/bg-shuttle.png"
          ></image>
          <image
            class="float-menu-btn"
            referrerpolicy="no-referrer"
            style="width: 77px; height: 66px"
            src="@/assets/images/icon-fly-ship.png"
          >
          </image>
        </view>
      </template>
      <template #menu-list-item="{ index }">
        <image
          class="float-menu-item"
          @tap="itemTap"
          :src="`https://susuanqiniu.knowbox.cn/fe/wx-shop/${menuItems[index]}.png`"
        ></image>
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
const menuItems = ref([
  "icon-my-book-space",
  "icon-my-book-talk",
  "icon-my-know-city",
]);
const floatMenu = ref();

const menuTap = () => {
  floatMenu.value.openOrClose();
};

const itemTap = () => {
  console.log("itemTap...");
};
</script>
<style lang="less">
.float-menu {
  display: flex;
  position: relative;
  width: 180px;
  height: 180px;
  .float-menu-bg {
    width: 180px;
    height: 180px;
    position: absolute;
  }

  .float-menu-btn {
    position: absolute;
    animation-name: fly-ship;
    animation-duration: 1.5s;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }
}
.float-menu-item {
  width: 128px;
  height: 128px;
}

@keyframes fly-ship {
  0% {
    transform: translate(0px, 0px);
  }
  20% {
    transform: translate(3px, -5px);
  }
  40% {
    transform: translate(6px, -10px);
  }
  60% {
    transform: translate(9px, -5px);
  }
  100% {
    transform: translate(0px, 0px);
  }
}
</style>
