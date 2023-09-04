<template>
  <view
    class="float-menu-root"
    :style="{
      '--distance': getSize(props.distance * 2),
    }"
  >
    <view style="z-index: 10">
      <slot name="float-menu" style="z-index: 10">
        <view class="float-menu-samples" style="width: 100rpx; height: 100rpx"
          >测试</view
        >
      </slot>
    </view>
    <view class="menu-list">
      <view
        class="menu-list-item"
        :class="{
          'animation-open': isMenuOpened,
          'animation-close': !isMenuOpened,
        }"
        :style="getItemStyle(index)"
        v-for="(item, index) in props.menuCount"
        :key="item"
      >
        <slot name="menu-list-item" :index="index"
          ><view
            style="
              width: 80rpx;
              height: 80rpx;
              text-align: center;
              line-height: 80rpx;
            "
            >{{ item }}</view
          ></slot
        >
      </view>
    </view>
  </view>
</template>
<script setup lang="ts">
import { ref } from "vue";
const props = defineProps({
  startDegree: {
    type: Number,
    default: -135,
  },
  stepDegree: {
    type: Number,
    default: -45,
  },
  menuCount: {
    type: Number,
    default: 3,
  },
  distance: {
    type: Number,
    default: 150,
  },
  unit: {
    type: String,
    default: "rpx",
  },
});
const isMenuOpened = ref(false);

const openOrClose = () => {
  isMenuOpened.value = !isMenuOpened.value;
};

const isOpen = () => {
  return isMenuOpened.value;
}

const getItemStyle = (index: number) => {
  const degree = props.startDegree + index * props.stepDegree;
  const x = Math.cos((degree * Math.PI) / 180) * props.distance;
  const y = Math.sin((degree * Math.PI) / 180) * props.distance;
  return {
    "transition-delay": index * 500 + "ms",
    opacity: isMenuOpened.value? 1: 0,
    transform: !isMenuOpened.value
      ? "translate(-50%, -50%)"
      : "translate(-50%, -50%) translate(" + x + "rpx, " + y + "rpx)",
  };
};

const getSize = (value: Number) => {
  return value + props.unit;
};

defineExpose({
  isOpen,
  openOrClose,
});
</script>
<style lang="scss">
.float-menu-root {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;

  .float-menu-samples {
    background-color: transparent;
    border-radius: 50%;
    border-width: 10px;
    border-style: dashed;
    border-color: blue;
    background-color: blue;
    text-align: center;
    line-height: 100px;
    // z-index: 10;
  }
  .menu-list {
    width: var(--distance);
    height: var(--distance);
    position: absolute;
    // border-radius: 50%;
    // border-width: 10px;
    // border-style: dotted;
    // border-color: red;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);

    .menu-list-item {
      // background-color: chocolate;
      // border-radius: 50%;
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }

    .animation-open {
      transition-property: all;
      transition-duration: 500ms;
      transition-timing-function: ease-in-out;
    }

    .animation-close {
      transition-property: all;
      transition-duration: 500ms;
      transition-timing-function: ease-in-out;
    }
  }
}
</style>
