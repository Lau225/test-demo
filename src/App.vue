<template>
  <div class="apology-page">
    <!-- 飘落元素容器 -->
    <div ref="fallingContainer" class="falling-container"></div>

    <!-- 主体内容 -->
    <div class="container">
      <h1 class="title">致一只无意被伤害的小生命</h1>
      <p class="text">我并非有意，只是一时疏忽，</p>
      <p class="text">让你在路过路口时，遭遇了不幸。</p>
      <p class="text">一想到这件事，我就满心愧疚与不安。</p>

      <div class="candle">
        <div class="flame"></div>
      </div>

      <p class="text">愿你在另一个世界，</p>
      <p class="text">自由、安全、不再受伤害，</p>
      <p class="text">有青草、有露水、有温暖。</p>

      <h2 class="sorry">真的很对不起 🙏</h2>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const fallingContainer = ref(null)
let intervalId = null

// 生成飘落的叶子/水滴/飞鸟
function createFalling() {
  if (!fallingContainer.value) return
  
  const emojis = ['🍃', '🌿', '💧', '🕊️']
  const emoji = emojis[Math.floor(Math.random() * emojis.length)]

  const elem = document.createElement('div')
  elem.className = 'falling'
  elem.innerText = emoji
  elem.style.left = Math.random() * 100 + 'vw'
  elem.style.fontSize = Math.random() * 15 + 15 + 'px'
  elem.style.animationDuration = Math.random() * 6 + 8 + 's'

  fallingContainer.value.appendChild(elem)

  // 动画结束后移除
  setTimeout(() => {
    elem?.remove()
  }, 14000)
}

// 挂载时启动动画
onMounted(() => {
  intervalId = setInterval(createFalling, 1500)
})

// 销毁时清除定时器
onUnmounted(() => {
  if (intervalId) clearInterval(intervalId)
})
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.apology-page {
  min-height: 100vh;
  background: linear-gradient(to bottom, #1a1a2e, #16213e);
  color: #f0f0f0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow-x: hidden;
  padding: 20px;
  position: relative;
}

.falling-container {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}

.container {
  max-width: 700px;
  text-align: center;
  position: relative;
  z-index: 2;
}

/* 飘落动画 */
.falling {
  position: absolute;
  top: -10%;
  opacity: 0.6;
  animation: fall linear infinite;
}

@keyframes fall {
  0% {
    transform: translate(0, 0) rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 0.8;
  }
  90% {
    opacity: 0.6;
  }
  100% {
    transform: translate(50px, 100vh) rotate(720deg);
    opacity: 0;
  }
}

/* 文字渐显 */
.title {
  font-size: 32px;
  margin-bottom: 30px;
  opacity: 0;
  animation: fadeIn 2s ease forwards 0.5s;
  color: #e0e0e0;
}

.text {
  font-size: 18px;
  line-height: 1.8;
  margin-bottom: 20px;
  opacity: 0;
  animation: fadeIn 2s ease forwards 1.2s;
  color: #d0d0d0;
}

.sorry {
  font-size: 22px;
  margin-top: 40px;
  color: #a8d8ea;
  opacity: 0;
  animation: fadeIn 2s ease forwards 2s;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}

/* 烛光 */
.candle {
  width: 16px;
  height: 50px;
  background: #fff;
  border-radius: 4px;
  margin: 40px auto 20px;
  position: relative;
  opacity: 0;
  animation: fadeIn 2s ease forwards 1.5s;
}

.flame {
  position: absolute;
  top: -22px;
  left: 50%;
  transform: translateX(-50%);
  width: 12px;
  height: 25px;
  background: #ffaa00;
  border-radius: 50% 50% 20% 20%;
  animation: flicker 1.5s infinite alternate ease-in-out;
}

@keyframes flicker {
  0% {
    transform: translateX(-50%) scale(1);
    opacity: 0.9;
  }
  100% {
    transform: translateX(-50%) scale(1.1);
    opacity: 0.7;
  }
}
</style>