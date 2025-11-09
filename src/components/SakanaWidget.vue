<template>
  <div ref="widgetTarget" class="sakana-widget" aria-label="Sakana widget" />
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";
import "sakana-widget/lib/index.css";
import SakanaWidget from "sakana-widget";

const widgetTarget = ref(null);
let widgetInstance = null;

const zmal = SakanaWidget.getCharacter('chisato');
zmal.image = `https://img.zmal.top/20250406/avatar.png`;
SakanaWidget.registerCharacter('zmal', zmal);

const mountWidget = () => {
  if (!widgetTarget.value) return;
  widgetInstance = new SakanaWidget({
    character: "zmal",
    autoFit: true
  })
  // .setState({r: 100 })
  .mount(widgetTarget.value);
};

onMounted(() => {
  mountWidget();
});

onBeforeUnmount(() => {
  widgetInstance?.unmount?.();
  widgetInstance = null;
});
</script>

<style scoped>
.sakana-widget {
  position: fixed;
  right: clamp(12px, 2vw, 32px);
  bottom: calc(46px + 12px);
  width: min(260px, 34vw);
  z-index: 5;
}

@media (max-width: 720px) {
  .sakana-widget {
    width: 180px;
    right: 16px;
    bottom: calc(46px + 16px);
  }
}

@media (max-width: 480px) {
  .sakana-widget {
    width: 150px;
    right: 12px;
    bottom: calc(46px + 16px);
  }
}
</style>
