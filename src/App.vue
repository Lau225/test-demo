<template>
  <div class="apology-page">
    <!-- 飘落祈福元素 -->
    <div ref="fallingContainer" class="falling-container"></div>

    <!-- 蛤蟆柔光背景 -->
    <div class="bg-frog">
      <svg viewBox="0 0 200 120" xmlns="http://www.w3.org/2000/svg">
        <path d="M60,80 Q80,50 120,80 Q150,100 180,90 Q160,110 100,110 Q40,110 60,80Z" fill="#3a4f4a" opacity="0.35"/>
        <circle cx="75" cy="70" r="4" fill="#5a726c" opacity="0.4"/>
        <circle cx="130" cy="72" r="4" fill="#5a726c" opacity="0.4"/>
      </svg>
    </div>

    <!-- 主内容区 -->
    <div class="container">
      <h1 class="title">致雨夜路边小蛙</h1>

      <p class="line line1">昨夜骑车疏忽</p>
      <p class="line line2">没能刹车，惊扰了你短暂的一生。</p>
      <p class="line line3">我看见你们结伴路过路口，</p>
      <p class="line line4">却偏偏让无辜的你，撞上我的疏忽。</p>

      <div class="candle">
        <div class="flame"></div>
      </div>

      <p class="line line5">我心里一直难过、愧疚，久久放不下。</p>
      <p class="line line6">你只是安稳赶路，想找一方湿润的泥土，</p>
      <p class="line line7">想躲风雨、想好好活着，从来没有错。</p>
      <p class="line line8">是我大意，是我慌张，没能护你周全。</p>

      <p class="line line9">愿去往彼岸的路上，没有车轮，没有惊扰，</p>
      <p class="line line10">有软软的青苔，清澈的露水，安静的晚风。</p>
      <p class="line line11">愿来生做一只自在无忧的小蛙，</p>
      <p class="line line12">日日栖于青草丛，夜夜安于月光下。</p>

      <h2 class="sorry">小蛙，真的很对不起 🙏</h2>
      <p class="bless">以此一念，为你祈福</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const fallingContainer = ref(null)
let timer = null

// 飘落落叶/水滴/白鸽动画
const createFall = () => {
  if (!fallingContainer.value) return
  const icons = ['🍃','🌿','💧','🕊️']
  const el = document.createElement('div')
  el.className = 'falling-item'
  el.innerText = icons[Math.floor(Math.random() * icons.length)]
  el.style.left = Math.random() * 100 + 'vw'
  el.style.fontSize = `${12 + Math.random() * 10}px`
  el.style.animationDuration = `${7 + Math.random() * 8}s`
  fallingContainer.value.appendChild(el)
  setTimeout(() => el.remove(), 15000)
}

onMounted(() => {
  timer = setInterval(createFall, 1800)
})
onUnmounted(() => {
  clearInterval(timer)
})
</script>

<style scoped>
/* 全局基础 - 移动端优先 */
.apology-page {
  min-height: 100vh;
  width: 100%;
  box-sizing: border-box;
  background: linear-gradient(180deg, #16202b 0%, #101a24 100%);
  position: relative;
  overflow-x: hidden;
  padding: 40px 20px 60px;
  font-family: "微软雅黑", system-ui, sans-serif;
}

/* 飘落层 */
.falling-container {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}
.falling-item {
  position: absolute;
  top: -8%;
  opacity: 0.5;
  animation: fallMove linear infinite;
}
@keyframes fallMove {
  0% {transform: translateY(0) rotate(0deg); opacity: 0;}
  15% {opacity: 0.7;}
  100% {transform: translateY(100vh) rotate(720deg); opacity: 0;}
}

/* 蛙背景 柔光低调 */
.bg-frog {
  position: absolute;
  bottom: 10%;
  left: 50%;
  transform: translateX(-50%);
  width: 60vw;
  max-width: 280px;
  z-index: 0;
  opacity: 0.25;
  filter: blur(2px);
}

/* 内容容器 移动端居中 */
.container {
  position: relative;
  z-index: 2;
  max-width: 520px;
  margin: 0 auto;
  text-align: center;
}

/* 标题动画 */
.title {
  font-size: clamp(22px, 5vw, 30px);
  color: #e6edf2;
  letter-spacing: 2px;
  margin-bottom: 35px;
  opacity: 0;
  animation: fadeIn 2s ease forwards 0.3s;
}

/* 逐行文字 + 阶梯延迟 */
.line {
  font-size: clamp(15px, 3.5vw, 17px);
  color: #c9d6df;
  line-height: 2;
  margin: 8px 0;
  opacity: 0;
  animation: fadeIn 1.8s ease forwards;
}
.line1 {animation-delay: 0.8s;}
.line2 {animation-delay: 1.3s;}
.line3 {animation-delay: 1.8s;}
.line4 {animation-delay: 2.3s;}
.line5 {animation-delay: 3s;}
.line6 {animation-delay: 3.5s;}
.line7 {animation-delay: 4s;}
.line8 {animation-delay: 4.5s;}
.line9 {animation-delay: 5.2s;}
.line10 {animation-delay: 5.7s;}
.line11 {animation-delay: 6.2s;}
.line12 {animation-delay: 6.7s;}

@keyframes fadeIn {
  to {opacity: 1;}
}

/* 烛光 */
.candle {
  width: 14px;
  height: 45px;
  background: #f8f8f8;
  border-radius: 3px;
  margin: 45px auto;
  position: relative;
  opacity: 0;
  animation: fadeIn 2s ease forwards 2.6s;
}
.flame {
  position: absolute;
  top: -20px;
  left: 50%;
  transform: translateX(-50%);
  width: 10px;
  height: 22px;
  background: linear-gradient(#ffcc44, #ff8822);
  border-radius: 50% 50% 25% 25%;
  animation: flicker 1.4s infinite alternate;
}
@keyframes flicker {
  0% {transform: translateX(-50%) scale(0.95); opacity: 0.85;}
  100% {transform: translateX(-50%) scale(1.08); opacity: 0.7;}
}

/* 结尾道歉 & 祈福 */
.sorry {
  font-size: clamp(18px, 4vw, 22px);
  color: #a0c8e4;
  margin-top: 40px;
  opacity: 0;
  animation: fadeIn 2s ease forwards 7.2s;
}
.bless {
  font-size: clamp(14px, 3vw, 16px);
  color: #89a3b4;
  margin-top: 15px;
  opacity: 0;
  animation: fadeIn 2s ease forwards 7.8s;
}
</style>