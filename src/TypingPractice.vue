<script setup>
import { ref, computed, onMounted } from 'vue'
const appVersion = __APP_VERSION__;

const defaults = [
  // 'Time flies fast.',
  // 'Short and sweet.',
  // 'Vue makes UI fun.',
  // 'Practice makes perfect.',
  // 'Type with steady rhythm.',
  // 'Small steps every day.',
  // 'Stay calm and type on.',
  // 'Accuracy over speed.',
  // 'Hands on home row.',
  // 'Breathe and relax.',
  '가는 날이 장날이다',
  '가는 말이 고와야 오는 말이 곱다',
  '가랑비에 옷 젖는 줄 모른다',
  '가랑잎이 솔잎더러 바스락거린다고 한다',
  '가재는 게 편이다',
  '가지 많은 나무에 바람 잘 날 없다',
  '간에 가서 붙고 쓸개에 가서 붙는다',
  '간에 기별도 안 간다',
  '간이 콩알만 해지다',
  '갈수록 태산',
  '같은 값이면 다홍치마',
  '개구리 올챙이 적 생각 못한다',
  '개밥에 도토리',
  '개천에서 용 난다',
  '고기는 씹어야 맛이요, 말은 해야 맛이라',
  '고래 싸움에 새우 등 터진다',
  '고양이 목에 방울 달기',
  '공든 탑이 무너지랴',
  '구더기 무서워 장 못 담글까',
  '구슬이 서 말이라도 꿰어야 보배라',
  '귀에 걸면 귀걸이, 코에 걸면 코걸이',
  '그림의 떡',
  '금강산도 식후경',
  '까마귀 날자 배 떨어진다',
  '꿩 대신 닭',
  '꿩 먹고 알 먹기',
  '남의 잔치에 감 놓아라 배 놓아라 한다',
  '낫 놓고 기역자도 모른다',
  '낮말은 새가 듣고 밤말은 쥐가 듣는다',
  '내 코가 석 자',
  '누워서 침 뱉기',
  '늦게 배운 도둑이 날 새는 줄 모른다',
  '다 된 죽에 코 풀기',
  '달면 삼키고 쓰면 뱉는다',
  '닭 잡아 먹고 오리발 내민다',
  '도둑이 제 발 저린다',
  '돌다리도 두들겨 보고 건너라',
  '되로 주고 말로 받는다',
  '등잔 밑이 어둡다',
  '땅 짚고 헤엄치기',
  '똥 묻은 개가 겨 묻은 개 나무란다',
  '뛰는 놈 위에 나는 놈 있다',
  '마른 하늘에 날벼락',
  '말 한마디에 천 냥 빚도 갚는다',
  '목구멍이 포도청이다',
  '못된 송아지 엉덩이에 뿔 난다',
  '믿는 도끼에 발등 찍힌다',
  '밑 빠진 독에 물 붓기',
  '바늘 도둑이 소 도둑 된다',
  '배보다 배꼽이 더 크다',
  '백지장도 맞들면 낫다',
  '벼룩의 간 빼먹기',
  '병 주고 약 준다',
  '보기 좋은 떡이 먹기도 좋다',
  '빛 좋은 개살구',
  '사공이 많으면 배가 산으로 올라간다',
  '새발의 피',
  '서당 개 삼 년에 풍월을 읊는다',
  '세 살 버릇 여든까지 간다',
  '소 잃고 외양간 고친다',
  '소문난 잔치에 먹을 것 없다',
  '쇠뿔도 단김에 빼랬다',
  '수박 겉 핥기',
  '식은 죽 먹기',
  '십 년이면 강산도 변한다',
  '싼 게 비지떡',
  '아는 길도 물어 가라',
  '아니 땐 굴뚝에 연기 나랴',
  '아닌 밤중에 홍두깨',
  '약방에 감초',
  '어물전 망신은 꼴뚜기가 시킨다',
  '열 길 물 속은 알아도 한 길 사람 속은 모른다',
  '열 번 찍어 아니 넘어가는 나무 없다',
  '오뉴월 감기는 개도 안 걸린다',
  '오르지 못할 나무는 쳐다보지도 말아라',
  '옥의 티',
  '우물에 가서 숭늉 찾는다',
  '울며 겨자 먹기',
  '원수는 외나무 다리에서 만난다',
  '원숭이도 나무에서 떨어진다',
  '윗물이 맑아야 아랫물도 맑다',
  '자라 보고 놀란 가슴 솥뚜껑 보고 놀란다',
  '자랄 나무는 떡잎부터 알아본다',
  '작은 고추가 더 맵다',
  '종로에서 뺨 맞고 한강 가서 눈 흘긴다',
  '좋은 약은 입에 쓰다',
  '쥐구멍에도 볕 들 날이 있다',
  '지렁이도 밟으면 꿈틀한다',
  '천 리 길도 한 걸음부터',
  '칼로 물 베기',
  '콩 심은 데 콩 나고 팥 심은 데 팥 난다',
  '티끌 모아 태산',
  '핑계 없는 무덤 없다',
  '하늘의 별 따기',
  '하늘이 무너져도 솟아날 구멍이 있다',
  '하룻강아지 범 무서운 줄 모른다',
  '한 귀로 듣고 한 귀로 흘린다',
  '한 술 밥에 배 부르랴',
  '함흥차사라',
  '호랑이도 제 말 하면 온다',
]

const sentences = ref([])
const currentIndex = ref(0)
const typed = ref('')
const started = ref(false)
const startTime = ref(null) // number | null
const endTime = ref(null)   // number | null
const correct = ref(0)
const total = ref(0)
const strictMode = ref(true)
const shuffle = ref(true)
const customText = ref('')
const inputElement = ref(null)
const isValidating = ref(false)

const currentSentence = computed(() => sentences.value[currentIndex.value] || '')
const currentSentenceChars = computed(() => currentSentence.value.split(''))
const totalChars = computed(() => currentSentence.value.length)

const elapsedMinutes = computed(() => {
  if (!started.value || !startTime.value) return 0
  const end = endTime.value ?? Date.now()
  const ms = Math.max(1, end - startTime.value)
  return ms / 60000
})

const wpm = computed(() => {
  if (!started.value) return 0
  const words = correct.value / 5
  return Math.round(words / Math.max(0.01, elapsedMinutes.value))
})

const accuracy = computed(() => {
  if (total.value === 0) return 100
  return Math.max(0, Math.round((correct.value / total.value) * 100))
})

const completed = computed(() =>
  typed.value === currentSentence.value && currentSentence.value.length > 0
)

function shuffleSentences() {
  sentences.value = [...sentences.value].sort(() => Math.random() - 0.5)
}

function initSentences() {
  const saved = localStorage.getItem('typing.sentences')
  if (saved) {
    try {
      sentences.value = JSON.parse(saved)
    } catch {
      sentences.value = [...defaults]
    }
  } else {
    sentences.value = [...defaults]
  }
  
  if (shuffle.value) {
    shuffleSentences()
  }
}

function start() {
  started.value = true
  startTime.value = Date.now()
  endTime.value = null
  typed.value = ''
  correct.value = 0
  total.value = 0
}

async function onInput() {
  if (!started.value) {
    start()
  }
  const target = currentSentence.value
  const t = typed.value

  total.value = t.length
  let c = 0
  for (let i = 0; i < Math.min(t.length, target.length); i++) {
    if (t[i] === target[i]) {
      c++
    }
  }
  
  // loose counts up to sentence len; strict penalizes extra chars
  correct.value = strictMode.value ? c - Math.max(0, t.length - target.length) : c
  if (correct.value < 0) {
    correct.value = 0
  }

  if (t.length >= target.length) {
    endTime.value = Date.now()
  } else {
    endTime.value = null
  }

  if (hasErrorOnLastInput()) {
    beep()
    return
  }
  
  await goNextIfCorrect()
} 

function onEnter(event) {
  // goNextIfCorrect()
}

function onKeyDown(event) {
  if (event.key === 'Backspace') {
    // Update counter or warning states
    isValidating.value = false
    return
  }

  isValidating.value = true 
}

function onDelete(event) {
  // console.log("🚀 ~ onDelete ~ event:", event)
  
} 
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

function wait1Second() {
  return new Promise(resolve => {
    setTimeout(resolve, 1000)
  })
}

async function dingDong() {
  await delay(200)     // Short pause
  beep(300, 800, 0.3)  // "Ding" - higher pitch
  await delay(200)     // Short pause
  beep(330, 600, 0.3)  // "Dong" - lower pitch
}

async function goNextIfCorrect () {
  if (typed.value === currentSentence.value) { 
    await dingDong()
    next()
  }
}

function next() {
  if (currentIndex.value < sentences.value.length - 1) {
    currentIndex.value++
  } else {
    if (shuffle.value) {
      shuffleSentences()
    }
    currentIndex.value = 0
  }
  started.value = false
  typed.value = ''
  startTime.value = null
  endTime.value = null
  correct.value = 0
  total.value = 0

  inputElement.value.focus()
}

function resetAll() {
  currentIndex.value = 0
  started.value = false
  typed.value = ''
  startTime.value = null
  endTime.value = null
  correct.value = 0
  total.value = 0
}


function hasErrorOnLastInput() {
  if (isValidating.value === false) {
    return
  }
  const t = typed.value
  const i = t.length - 1

  // all good and last one is space to progress next one
  if (currentSentence.value[i] === undefined && t[i] === ' ') {
    return false
  }
  const rVal = t[i] !== currentSentence.value[i]
  return rVal
}

function charClass(i) {
  const t = typed.value
  if (i < t.length) {
    return t[i] === currentSentence.value[i] ? 'correct' : 'incorrect'
  }
  if (i === t.length && started.value && !completed.value) return 'current'
  return ''
}

function toggleMode() {
  strictMode.value = !strictMode.value
}

function loadDefaults() {
  customText.value = defaults.join('\n')
}

function applyCustom() {
  const lines = (customText.value || '')
    .split(/\n+/)
    .map(s => s.trim())
    .filter(Boolean)
  sentences.value = lines.length ? lines : [...defaults]
  localStorage.setItem('typing.sentences', JSON.stringify(sentences.value))
  resetAll()
}

function clearCustom() {
  customText.value = ''
  localStorage.removeItem('typing.sentences')
  sentences.value = [...defaults]
  resetAll()
}

function beep(duration = 200, frequency = 440, volume = 1) {
  const ctx = new (window.AudioContext || window.webkitAudioContext)()
  const oscillator = ctx.createOscillator()
  const gainNode = ctx.createGain()

  oscillator.connect(gainNode)
  gainNode.connect(ctx.destination)

  oscillator.type = "sine"      // wave type: sine, square, triangle, sawtooth
  oscillator.frequency.value = frequency
  gainNode.gain.value = volume

  oscillator.start()
  setTimeout(() => {
    oscillator.stop()
    ctx.close()
  }, duration)
}


onMounted(() => {
  document.title = `아버지를 위한 타자 연습 v${appVersion}`
  initSentences()
})

</script>


<template>
  <div class="wrap">
    <div class="card">
      <h1>아버지를 위한 타자 연습 v{{appVersion}}</h1>
      <!-- <div class="muted">Practice short sentences. Built with Vue 3 (Composition API).</div> -->

      <div class="stats">
        <div class="stat"><div class="k">타자속도</div><div class="v">{{ wpm }}</div></div>
        <div class="stat"><div class="k">정확도</div><div class="v">{{ accuracy }}%</div></div>
        <div class="stat"><div class="k">글자수</div><div class="v">{{ typed?.length }}/{{ totalChars }}</div></div>
        <div class="stat"><div class="k">문장</div><div class="v">{{ currentIndex + 1 }} / {{ sentences?.length }}</div></div>
      </div>

      <div class="target" role="region" aria-live="polite">
        <span
          v-for="(ch, i) in currentSentenceChars"
          :key="i"
          class="char"
          :class="charClass(i)"
        >
          <pre>{{ ch }}</pre>
        </span>
      </div>

      <div style="margin:10px 0"></div>
      <input
        ref="inputElement"
        class="input"
        type="text"
        v-model="typed"
        :spellcheck="false"
        autocorrect="off"
        :placeholder="started ? '계속 입력하세요...' : '시작 버튼을 누르거나 입력을 시작하세요'"
        @input="onInput"
        @keydown="onKeyDown"
        @keydown.enter.prevent="onEnter"
        @keydown.delete="onDelete"
        :disabled="false && completed"
        autofocus
      />

      <div style="margin:12px 0" class="row">
        <button class="btn" @click="start" :disabled="started && !completed">시작</button>
        <button class="btn" @click="next" :disabled="!started">다음</button>
        <button class="btn secondary" @click="resetAll">초기화</button>
        <label class="pill">
          <input type="checkbox" v-model="shuffle" />
          섞기
        </label>
        <span class="pill">{{ strictMode ? '엄격한 모드' : '느슨한 모드' }}</span>
        <button class="btn secondary" @click="toggleMode">모드 바꾸기</button>
      </div>

      <!-- <details>
        <summary>Customize sentences</summary>
        <div class="cfg">
          <div>
            <div class="small">One per line. Your list is saved in your browser.</div>
            <textarea v-model="customText" placeholder="Type each sentence on a new line"></textarea>
          </div>
          <div class="flex" style="flex-direction:column; gap:10px;">
            <button class="btn" @click="loadDefaults">Load defaults</button>
            <button class="btn" @click="applyCustom">Apply</button>
            <button class="btn secondary" @click="clearCustom">Clear</button>
          </div>
        </div>
        <ul class="list">
          <li v-for="(s, i) in sentences" :key="'s-'+i">{{ s }}</li>
        </ul>
      </details> -->

      <details style="margin-top:10px;">
        <summary>팁</summary>
        <ul class="list">
          <li><b>엄격한</b> 모드는 정확히 일치해야 하고 <b>느슨한</b> 모드는 실수가 있어도 계속 진행할 수 있습니다.</li>
          <li>문장을 다 입력하면 <b>Enter</b> 키를 눌러 다음으로 넘어가세요.</li>
        </ul>
      </details>
    </div>
  </div>
</template>

<style>
:root {
  color-scheme: light dark;
}
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto,
    "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
  background: #0b1020;
  color: #e9eefc;
  min-height: 100vh;
  display: grid;
  /* place-items: center; */
}
.wrap {
  width: max(980px, 100%);
  padding: 50px;
}
.card {
  background: #111735;
  border: 1px solid #1a2250;
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
}
h1 {
  margin: 0 0 6px;
  font-size: 22px;
}
.muted {
  color: #9fb0ff;
  font-size: 13px;
}
.row {
  display: flex;
  gap: 12px;
  align-items: center;
  flex-wrap: wrap;
}
.btn {
  border: 1px solid #2a3a8a;
  background: #1b2360;
  color: #e9eefc;
  padding: 10px 14px;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
}
.btn.secondary {
  background: transparent;
}
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
.input {
  width: 100%;
  padding: 14px 12px;
  border-radius: 12px;
  border: 1px solid #23307a;
  background: #0f1640;
  color: #e9eefc;
  font-size: 24px;
}
.target {
  font-size: 36px;
  line-height: 1.8;
  background: #0e1538;
  padding: 14px;
  border-radius: 12px;
  border: 1px dashed #2a3a8a;
  min-height: 64px;
}
.char {
  display: inline-block;
  padding: 2px 0;
  border-bottom: 2px solid transparent;
}
.char.correct {
  color: #9df3b2;
  border-bottom-color: #9df3b2;
}
.char.incorrect {
  color: #ff9aa7;
  border-bottom-color: #ff9aa7;
}
.char.current {
  background: #20308f;
  border-radius: 4px;
}
.stats {
  display: grid;
  grid-template-columns: repeat(4, minmax(120px, 1fr));
  gap: 10px;
  margin: 12px 0;
}
.stat {
  background: #0f1640;
  border: 1px solid #23307a;
  border-radius: 12px;
  padding: 10px 12px;
}
.stat .k {
  font-size: 13px;
  color: #9fb0ff;
}
.stat .v {
  font-weight: 700;
  font-size: 22px;
}
.flex {
  display: flex;
  gap: 8px;
  align-items: center;
}
.pill {
  font-size: 12px;
  padding: 6px 10px;
  border-radius: 999px;
  border: 1px solid #2a3a8a;
}
details {
  background: #0e1538;
  border: 1px solid #1a2250;
  border-radius: 12px;
  padding: 10px 12px;
}
summary {
  cursor: pointer;
  font-weight: 600;
}
.list {
  margin: 6px 0 0;
  padding-left: 16px;
}
.list li {
  margin: 4px 0;
}
.cfg {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 10px;
  align-items: start;
}
.small {
  font-size: 12px;
  color: #9fb0ff;
}
textarea {
  width: 100%;
  min-height: 90px;
  padding: 10px;
  border-radius: 12px;
  border: 1px solid #23307a;
  background: #0f1640;
  color: #e9eefc;
}

</style>
