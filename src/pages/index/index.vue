<template>
  <view class="index">
    <!-- <Counter /> -->
    <float-menu :distance="200">
      <template #float-menu>
        <view
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

<script>
import "./index.scss";
import FloatMenu from "@/components/FloatMenu.vue";
// import Counter from "../../components/Counter.vue";

export default {
  name: "IndexPage",
  components: {
    FloatMenu,
  },
};
</script>
