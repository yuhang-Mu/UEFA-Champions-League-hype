<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue'

const menuOpen = ref(false)
const now = ref(new Date())
const matchTime = new Date('2027-06-05T20:00:00+02:00')
let timer

const countdown = computed(() => {
  const remaining = Math.max(0, matchTime.getTime() - now.value.getTime())
  const days = Math.floor(remaining / 86400000)
  const hours = Math.floor((remaining % 86400000) / 3600000)
  const minutes = Math.floor((remaining % 3600000) / 60000)
  const seconds = Math.floor((remaining % 60000) / 1000)
  return [days, hours, minutes, seconds].map((value) => String(value).padStart(2, '0'))
})

onMounted(() => { timer = setInterval(() => { now.value = new Date() }, 1000) })
onUnmounted(() => clearInterval(timer))
</script>

<template>
  <main class="poster" id="top">
    <div class="grain" aria-hidden="true"></div>
    <header class="topbar">
      <a class="brand" href="#top" aria-label="欧冠主页">
        <span class="brand-star">✳</span>
        <span>CHAMPIONS<br /><b>LEAGUE</b></span>
      </a>
      <button class="menu-toggle" :aria-expanded="menuOpen" aria-label="切换导航" @click="menuOpen = !menuOpen"><span></span><span></span></button>
      <nav :class="{ open: menuOpen }">
        <a href="#story" @click="menuOpen = false">赛事故事</a>
        <a href="#venue" @click="menuOpen = false">决赛之城</a>
        <a class="nav-ticket" href="#ticket" @click="menuOpen = false">锁定席位 <span>↗</span></a>
      </nav>
    </header>

    <section class="hero" id="story">
      <div class="hero-copy">
        <p class="eyebrow"><span class="live-dot"></span> 2026 / 27 · THE FINAL</p>
        <h1>为荣耀<br /><em>而战。</em></h1>
        <p class="intro">九十分钟，决定一个时代。<br />欧洲之巅，等你亲眼见证。</p>
        <a class="cta" href="#ticket"><span>进入决赛之夜</span><b>↗</b></a>
        <div class="edition"><span class="edition-line"></span><span>欧洲冠军联赛 · 第 72 届</span></div>
      </div>

      <div class="visual" aria-label="星空球场中的冠军奖杯插画">
        <div class="orbit orbit-one"></div><div class="orbit orbit-two"></div>
        <div class="spark spark-a">✦</div><div class="spark spark-b">✧</div><div class="spark spark-c">✦</div>
        <div class="stadium-glow"></div>
        <div class="stadium"><div class="stands"></div><div class="pitch"></div><div class="crowd-lights"></div></div>
        <div class="cup-shadow"></div>
        <div class="trophy">
          <div class="handle handle-left"></div><div class="handle handle-right"></div>
          <div class="cup-bowl"><div class="cup-shine"></div></div>
          <div class="cup-stem"></div><div class="cup-base"></div><div class="cup-foot"></div>
        </div>
        <div class="visual-caption"><span>THE ROAD TO</span><b>GLORY</b><i>✳</i></div>
        <div class="side-note">ONE NIGHT<br />ONE DREAM</div>
      </div>
      <div class="vertical-label">UEFA CHAMPIONS LEAGUE <span>✳</span> 2027</div>
    </section>

    <section class="event-strip" id="venue">
      <div class="event-place"><span class="mini-label">THE FINAL · 2027</span><strong>布达佩斯</strong><span class="place-en">BUDAPEST, HUNGARY</span></div>
      <div class="event-date"><span class="mini-label">决赛开球</span><strong>06<span>.</span>05</strong><span class="place-en">PUSKÁS ARÉNA</span></div>
      <div class="countdown-wrap"><span class="mini-label">距离决赛还有</span><div class="countdown"><span v-for="(unit, index) in countdown" :key="index"><b>{{ unit }}</b><small>{{ ['天', '时', '分', '秒'][index] }}</small></span></div></div>
      <div class="event-star">✳</div>
    </section>

    <footer class="footer" id="ticket">
      <span>THE BEAUTIFUL GAME. THE BIGGEST STAGE.</span>
      <a href="mailto:tickets@example.com?subject=Champions%20League%20Final%20Tickets">加入决赛候补名单 <b>↗</b></a>
      <span class="footer-mark">UCL <i>✳</i> 2027</span>
    </footer>
  </main>
</template>
