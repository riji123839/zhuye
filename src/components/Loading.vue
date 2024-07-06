<template>
  <div id="loader-wrapper" :class="store.imgLoadStatus ? 'loaded' : null">
    <div class="loader">
      <div class="loader-sphere">
        <div class="loader-circle loader-circle1"></div>
        <div class="loader-circle loader-circle2"></div>
        <div class="loader-circle loader-circle3"></div>
      </div>
      <div class="loader-text">
        <span class="name">{{ siteName }}</span>
        <span class="tip">加载中</span>
      </div>
    </div>
    <div class="loader-section section-left"></div>
    <div class="loader-section section-right"></div>
  </div>
</template>

<script setup>
import { mainStore } from "@/store";

const store = mainStore();

// 配置
const siteName = import.meta.env.VITE_SITE_NAME;
</script>

<style lang="scss" scoped>
#loader-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 999;
  overflow: hidden;
  .loader {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .loader-sphere {
      width: 150px;
      height: 150px;
      position: relative;
      perspective: 1000px;
      .loader-circle {
        width: 100%;
        height: 100%;
        border-radius: 50%;
        position: absolute;
        border: 3px solid transparent;
        border-top-color: #fff;
      }
      .loader-circle1 {
        animation: spin-sphere 1.8s linear infinite;
      }
      .loader-circle2 {
        border-top-color: #a4a4a4;
        animation: spin-sphere-reverse 0.6s linear infinite;
        transform: rotateX(90deg);
      }
      .loader-circle3 {
        border-top-color: #d3d3d3;
        animation: spin-sphere 1s linear infinite;
        transform: rotateY(90deg);
      }
    }
    .loader-text {
      display: flex;
      flex-direction: column;
      align-items: center;
      color: #fff;
      z-index: 2;
      margin-top: 40px;
      font-size: 24px;
      .tip {
        margin-top: 6px;
        font-size: 18px;
        opacity: 0.6;
      }
    }
  }
  .loader-section {
    position: fixed;
    top: 0;
    width: 51%;
    height: 100%;
    background: #333;
    z-index: 1;
    &.section-left {
      left: 0;
    }
    &.section-right {
      right: 0;
    }
  }
  &.loaded {
    visibility: hidden;
    transform: translateY(-100%);
    transition:
      transform 0.3s 1s ease-out,
      visibility 0.3s 1s ease-out;
    .loader {
      .loader-sphere,
      .loader-text {
        opacity: 0;
        transition: opacity 0.3s ease-out;
      }
    }
    .loader-section {
      &.section-left {
        transform: translateX(-100%);
        transition: transform 0.5s 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
      }
      &.section-right {
        transform: translateX(100%);
        transition: transform 0.5s 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
      }
    }
  }
}

@keyframes spin-sphere {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes spin-sphere-reverse {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}
</style>

