<template>
  <div id="loader-wrapper" :class="store.imgLoadStatus ? 'loaded' : null">
    <div class="loader">
      <div class="inner one"></div>
      <div class="inner two"></div>
      <div class="inner three"></div>
    </div>
    <div class="loader-text">
      <span class="name">{{ siteName }}</span>
      <span class="tip">加载中</span>
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
    position: absolute;
    top: 50%;
    left: 50%;
    width: 64px;
    height: 64px;
    border-radius: 50%;
    perspective: 800px;
    transform: translate(-50%, -50%);

    .inner {
      position: absolute;
      box-sizing: border-box;
      width: 100%;
      height: 100%;
      border-radius: 50%;
    }

    .one {
      left: 0%;
      top: 0%;
      animation: rotate-one 1s linear infinite;
      border-bottom: 3px solid #EFEFFA;
    }

    .two {
      right: 0%;
      top: 0%;
      animation: rotate-two 1s linear infinite;
      border-right: 3px solid #EFEFFA;
    }

    .three {
      right: 0%;
      bottom: 0%;
      animation: rotate-three 1s linear infinite;
      border-top: 3px solid #EFEFFA;
    }
  }

  .loader-text {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #fff;
    margin-top: 40px;
    font-size: 24px;
    .tip {
      margin-top: 6px;
      font-size: 18px;
      opacity: 0.6;
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
    .loader,
    .loader-text {
      opacity: 0;
      transition: opacity 0.3s ease-out;
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

@keyframes rotate-one {
  0% {
    transform: rotateX(35deg) rotateY(-45deg) rotateZ(0deg);
  }
  100% {
    transform: rotateX(35deg) rotateY(-45deg) rotateZ(360deg);
  }
}

@keyframes rotate-two {
  0% {
    transform: rotateX(50deg) rotateY(10deg) rotateZ(0deg);
  }
  100% {
    transform: rotateX(50deg) rotateY(10deg) rotateZ(360deg);
  }
}

@keyframes rotate-three {
  0% {
    transform: rotateX(35deg) rotateY(55deg) rotateZ(0deg);
  }
  100% {
    transform: rotateX(35deg) rotateY(55deg) rotateZ(360deg);
  }
}
</style>
