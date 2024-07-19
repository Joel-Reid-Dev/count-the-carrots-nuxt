<template>
  <div class="canvas-container">
    <canvas ref="canvas"></canvas>
  </div>
</template>

<script lang="ts">
import {defineProps} from 'vue';
interface Props {
  difficulty: string;
}

const props = defineProps<Props>();
const canvas = ref<HTMLCanvasElement | null>(null);
let ctx: CanvasRenderingContext2D | null = null;
let gameStarted = ref(false);
let imageCounts: { [key: string]: number } = {};
let items: any[] = [];

const logCounts = () => {
  for (let name in imageCounts) {
    console.log(`Image: ${name}, Total: ${imageCounts[name]}`);
  }
};

const drawItem = (item: any) => {
  if (ctx) {
    ctx.save();
    ctx.translate(item.x + item.width / 2, item.y + item.height / 2);
    ctx.rotate(item.rotation);
    ctx.drawImage(item.img, -item.width / 2, -item.height / 2, item.width, item.height);
    ctx.restore();
  }
};

const updateItem = (item: any, index: number) => {
  item.x += item.speedX;
  item.y += item.speedY;
  item.rotation += item.rotationSpeed;

  if (item.x > window.innerWidth || item.y > window.innerHeight || item.x < 0 || item.y < 0) {
    item.count++;

    if (item.count >= item.total) {
      items.splice(index, 1);
    } else {
      item.x = item.x > window.innerWidth ? 0 : (item.x < 0 ? window.innerWidth : item.x);
      item.y = item.y > window.innerHeight ? 0 : (item.y < 0 ? window.innerHeight : item.y);
    }
  }
};

const animate = () => {
  if (ctx && canvas.value && gameStarted.value) {
    //wipe the canvas clean :)
    ctx.clearRect(0, 0, canvas.value.width, canvas.value.height);

    for (let [index, item] of items.entries()) {
      updateItem(item, index);
      drawItem(item);
    }
    if (items.length === 0) {
      alert('Finished');
      gameStarted.value = false;
    } else {
      requestAnimationFrame(animate);
    }
  }
};

onMounted(() => {
  let imageNames = ['charizard.gif', 'pikachu.jpg', 'heracross.webp'];

  imageNames.forEach(name => {
    imageCounts[name] = Math.floor(Math.random() * 13) + 1;
    for (let i = 0; i < imageCounts[name]; i++) {
      let x = Math.random() * window.innerWidth;
      let y = Math.random() * (window.innerHeight * 0.5) + window.innerHeight * 0.25;
      let speedX = x < window.innerWidth / 2 ? Math.random() + 0.5 : -Math.random() - 0.5;
      if (props.difficulty == 'hard') {
        speedX *= 2;
      }
      let speedY = 0;
      let rotationSpeed = speedX > 0 ? -0.05 : 0.05;

      let img = new Image();
      img.onload = () => {
        items.push({
          x: x,
          y: y,
          speedX: speedX,
          speedY: speedY,
          img: img,
          width: 50,
          height: 50,
          rotation: 0,
          rotationSpeed: rotationSpeed,
          count: 0,
          total: Math.floor(Math.random() * 12) + 1,
          name: name
        });
      };
      img.src = name;
    }
  });
  if (canvas.value) {
    canvas.value.width = window.innerWidth;
    canvas.value.height = window.innerHeight;

    ctx = canvas.value.getContext('2d');
    gameStarted.value = true;
    logCounts();
    animate();
  }
});
export default {
  setup() {
    return {canvas};
  },
};
</script>

<style scoped lang="scss">
.canvas-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 60rem;
  height: 40rem;
  background-color: #f0f0f0;
  overflow: hidden;
  margin: 0 auto;
}

canvas {
  height: 100%;
  width: 100%;
}
</style>
