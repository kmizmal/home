<template>
  <div class="friend-card" @click="openLink">
    <img :src="friend.avatar" alt="Avatar" class="avatar" />
    <div class="info">
      <h3>{{ friend.name }}</h3>
      <p class="description">{{ friend.description }}</p>
      <!-- <a v-if="friend.link" :href="friend.link" target="_blank" @click.stop>Visit</a>
      <a v-else href="javascript:void(0);" style="color: gray; cursor: not-allowed"></a> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "FriendCard",
  props: {
    friend: {
      type: Object,
      required: true,
      default: () => ({
        avatar: "",
        name: "zmal的好朋友",
        description: "暂无描述",
        link: "#",
      }),
    },
  },
  methods: {
    openLink() {
      if (this.friend.link) {
        window.open(this.friend.link, "_blank");
      } else {
        console.warn("链接不存在");
      }
    },
  },
};
</script>

<style scoped>
.friend-card {
  position: relative;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  overflow: hidden;
  cursor: pointer;
  background: linear-gradient(45deg, #b0d8e540 30%, #786094 100%);
  transform-origin: center center;
  will-change: transform;
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: inherit;
    opacity: 0;
    transition: opacity 0.5s;
  }

  &:hover {
    width: 280px;
    height: 120px;
    border-radius: 12px;
    z-index: 100;
    transform: scale(1.2) translateY(-10px) translateZ(0);

    &::before {
      opacity: 1;
    }
  }
}

.avatar {
  position: absolute;
  top: 50%;
  left: 50%;
  height: 100%;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: all 0.3s 0.1s;
  border: 2px solid #fff;
}

.friend-card:hover .avatar {
  width: 60px;
  height: 60px;
  top: 20px;
  left: 20px;
  transform: none;
}

.info {
  opacity: 0;
  visibility: hidden;
  padding: 15px;
  transform: translateX(-20px);
  transition: all 0.3s 0.2s;
}

.friend-card:hover .info {
  opacity: 1;
  visibility: visible;
  transform: translateX(0);
  margin-left: 80px;
}

.description {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s 0.3s;
}

.friend-card:hover .description {
  max-height: 4em;
}

h3 {
  color: #fff;
}

/* 响应式调整 */
@media (max-width: 768px) {
  .friend-card:hover {
    transform: scale(1.1) translateY(-5px);
    width: 240px;
  }
}

</style>
