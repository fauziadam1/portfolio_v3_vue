<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const props = defineProps({
  squareSize: { type: Number, default: 2 },
  gridGap: { type: Number, default: 2 },
  flickerChance: { type: Number, default: 0.3 },
  maxOpacity: { type: Number, default: 0.3 },
  class: { type: String, default: "" },
});

const canvas = ref(null);
const container = ref(null);
let frame = 0;
let resizeObserver;

function draw() {
  const el = canvas.value;
  const wrap = container.value;
  const ctx = el?.getContext("2d");
  if (!el || !wrap || !ctx) return;

  const dpr = window.devicePixelRatio || 1;
  const width = wrap.clientWidth;
  const height = wrap.clientHeight;
  el.width = width * dpr;
  el.height = height * dpr;
  el.style.width = `${width}px`;
  el.style.height = `${height}px`;
  ctx.clearRect(0, 0, el.width, el.height);

  const computed = getComputedStyle(document.documentElement).getPropertyValue("--foreground");
  ctx.fillStyle = computed || "rgb(0,0,0)";

  const step = props.squareSize + props.gridGap;
  for (let x = 0; x < width; x += step) {
    for (let y = 0; y < height; y += step) {
      if (Math.random() < props.flickerChance) {
        ctx.globalAlpha = Math.random() * props.maxOpacity;
        ctx.fillRect(x * dpr, y * dpr, props.squareSize * dpr, props.squareSize * dpr);
      }
    }
  }
  frame = window.requestAnimationFrame(draw);
}

onMounted(() => {
  resizeObserver = new ResizeObserver(draw);
  if (container.value) resizeObserver.observe(container.value);
  draw();
});

onBeforeUnmount(() => {
  cancelAnimationFrame(frame);
  resizeObserver?.disconnect();
});
</script>

<template>
  <div ref="container" :class="['h-full w-full', props.class]">
    <canvas ref="canvas" class="pointer-events-none" />
  </div>
</template>
