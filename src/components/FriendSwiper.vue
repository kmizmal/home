<template>
  <Swiper
    class="friend-swiper"
    v-if="friends[0]"
    :modules="[Pagination, Mousewheel]"
    :slides-per-view="1"
    :space-between="20"
    :pagination="{
      el: '.swiper-pagination',
      clickable: true,
      bulletElement: 'div',
    }"
    :mousewheel="true"
  >
    <SwiperSlide v-for="(friend, index) in friends" :key="index">
      <div class="friend-card card" @click="openLink(friend.link)">
        <img :src="friend.avatar" alt="Avatar" class="avatar" />
        <div class="info">
          <h3>{{ friend.name }}</h3>
          <p class="description">{{ friend.description }}</p>
        </div>
      </div>
    </SwiperSlide>
  </Swiper>
  <div class="swiper-pagination"></div>
  <button @click="emit('closefriend')">关闭</button>
</template>

<script setup>
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Mousewheel } from "swiper/modules";
import "swiper/css";
import "swiper/css/pagination";

// 假设链接数据结构如下
import friends from "@/assets/friendLinks.json";

function openLink(link) {
  if (link) {
    window.open(link, "_blank");
  } else {
    console.warn("链接不存在");
  }
}
const emit = defineEmits(["closefriend"]);
</script>
<style lang="scss" scoped>
.friend-swiper {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding-bottom: 40px;

  .swiper-slide {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .friend-card {
    display: flex;
    align-items: center;
    position: relative;
    width: 260px;
    height: 120px;
    background: linear-gradient(45deg, #b0d8e540 30%, #786094 100%);
    transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    transform-origin: center;
    cursor: pointer;

    &:hover {
      .description {
        opacity: 1;
        visibility: visible;
        max-height: 4em;
      }
    }

    .avatar {
      position: absolute;
      left: 15px;
      top: 50%;
      transform: translateY(-50%);
      height: 60px;
      width: 60px;
      border-radius: 50%;
      border: 2px solid #fff;
      transition: all 0.3s 0.1s;
    }

    .info {
      margin-left: 80px;
      padding: 15px;
      transition: all 0.3s 0.2s;
    }

    .description {
      max-height: 0;
      opacity: 0;
      visibility: hidden;
      overflow: hidden;
      transition: max-height 0.3s 0.3s;
    }

    @media (hover: hover) {
      &:hover {
        transform: scale(1.2) translateY(-10px);
        border-radius: 12px;
        z-index: 100;
      }
    }
  }
  .swiper {
    left: -10px;
    width: calc(100% + 20px);
    padding: 5px 10px 0;
    z-index: 0;
    .swiper-slide {
      height: 100%;
    }
    .swiper-pagination {
      margin-top: 12px;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;
      :deep(.swiper-pagination-bullet) {
        background-color: #fff;
        width: 20px;
        height: 4px;
        margin: 0 4px;
        border-radius: 4px;
        opacity: 0.2;
        transition: opacity 0.3s;
        &.swiper-pagination-bullet-active {
          opacity: 1;
        }
        &:hover {
          opacity: 1;
        }
      }
    }
  }
}
</style>
