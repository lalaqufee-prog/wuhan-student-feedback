<script setup>
import { computed, reactive, ref } from 'vue'

const highlights = [
  '记录每天学了什么，复盘更清晰',
  '作业进度一眼可见，不再忘记提交',
  '把校园趣事和活动也留下来'
]

const activities = [
  { title: '升旗与晨会', time: '07:30', tag: '校园日常' },
  { title: '大课间跑操', time: '09:40', tag: '活力时间' },
  { title: '社团或班会', time: '16:20', tag: '校园活动' }
]

const moodOptions = ['超有精神', '状态不错', '平平稳稳', '有点疲惫']

const form = reactive({
  studentName: '李同学',
  className: '七年级（2）班',
  mood: '状态不错',
  studySummary: '今天复习了数学有理数运算，英语背诵了课文重点句型，语文完成了古诗文默写。',
  homeworkList: '数学练习册 2 页；英语单词抄写 1 遍；语文阅读理解 1 篇。',
  completion: 78,
  schoolActivities: '今天参加了午间阅读分享，班主任提醒大家准备周五的科技节展示。',
  funMoments: '课间和同桌一起讨论科学小实验，发现纸桥居然能承重好多本书。',
  needHelp: '英语完形填空还是有些慢，希望老师推荐练习方法。'
})

const submitted = ref(false)

const completionLabel = computed(() => {
  if (form.completion >= 90) return '完成得很棒'
  if (form.completion >= 70) return '进度不错'
  if (form.completion >= 50) return '还在稳步推进'
  return '需要再加把劲'
})

const summaryCards = computed(() => [
  { label: '今日学习', value: form.studySummary || '等待填写' },
  { label: '作业情况', value: form.homeworkList || '等待填写' },
  { label: '校园活动', value: form.schoolActivities || '等待填写' },
  { label: '有趣瞬间', value: form.funMoments || '等待填写' }
])

function submitForm() {
  submitted.value = true
}
</script>

<template>
  <div class="page-shell">
    <div class="bg-orb orb-a"></div>
    <div class="bg-orb orb-b"></div>
    <div class="bg-grid"></div>

    <main class="layout">
      <section class="hero card">
        <div class="hero-copy">
          <p class="eyebrow">Wuhan Campus Daily</p>
          <h1>江城少年每日反馈站</h1>
          <p class="hero-text">
            给武汉初中生准备的轻松反馈页，把今天的学习内容、作业进度、校园活动和有趣瞬间都装进一张卡片里。
          </p>
          <div class="hero-tags">
            <span v-for="item in highlights" :key="item">{{ item }}</span>
          </div>
        </div>

        <div class="hero-panel">
          <div class="sun"></div>
          <div class="hero-stat">
            <strong>{{ form.completion }}%</strong>
            <span>今日作业完成度</span>
          </div>
          <div class="hero-stat">
            <strong>{{ form.mood }}</strong>
            <span>现在的学习状态</span>
          </div>
        </div>
      </section>

      <section class="content-grid">
        <form class="card form-card" @submit.prevent="submitForm">
          <div class="section-heading">
            <div>
              <p class="mini-title">每日填写</p>
              <h2>今天的反馈内容</h2>
            </div>
            <span class="badge">一页完成</span>
          </div>

          <div class="form-grid">
            <label>
              <span>学生姓名</span>
              <input v-model="form.studentName" type="text" placeholder="请输入姓名" />
            </label>

            <label>
              <span>班级</span>
              <input v-model="form.className" type="text" placeholder="请输入班级" />
            </label>
          </div>

          <label>
            <span>今天的状态</span>
            <div class="mood-row">
              <button
                v-for="item in moodOptions"
                :key="item"
                class="mood-chip"
                :class="{ active: form.mood === item }"
                type="button"
                @click="form.mood = item"
              >
                {{ item }}
              </button>
            </div>
          </label>

          <label>
            <span>今天学了什么</span>
            <textarea
              v-model="form.studySummary"
              rows="4"
              placeholder="例如：数学复习了整式加减，英语听写了重点单词"
            />
          </label>

          <label>
            <span>今天有哪些作业</span>
            <textarea
              v-model="form.homeworkList"
              rows="4"
              placeholder="例如：数学练习册第 12 页，英语背诵第 3 课"
            />
          </label>

          <label>
            <span>作业完成情况：{{ form.completion }}%</span>
            <input v-model="form.completion" type="range" min="0" max="100" />
            <small>{{ completionLabel }}</small>
          </label>

          <label>
            <span>学校今天的活动</span>
            <textarea
              v-model="form.schoolActivities"
              rows="3"
              placeholder="例如：升旗仪式、阅读分享、班会、科技节彩排"
            />
          </label>

          <label>
            <span>今天最有趣的事情</span>
            <textarea
              v-model="form.funMoments"
              rows="3"
              placeholder="写下让你开心、惊讶或者觉得特别的一件事"
            />
          </label>

          <label>
            <span>需要老师或家长帮助的地方</span>
            <textarea
              v-model="form.needHelp"
              rows="3"
              placeholder="也可以写“暂时没有”"
            />
          </label>

          <button class="submit-btn" type="submit">生成今日反馈卡</button>
        </form>

        <div class="sidebar">
          <section class="card schedule-card">
            <div class="section-heading">
              <div>
                <p class="mini-title">校园节奏</p>
                <h2>常见日程提醒</h2>
              </div>
            </div>

            <div class="timeline">
              <article v-for="item in activities" :key="item.title" class="timeline-item">
                <strong>{{ item.time }}</strong>
                <div>
                  <h3>{{ item.title }}</h3>
                  <p>{{ item.tag }}</p>
                </div>
              </article>
            </div>
          </section>

          <section class="card preview-card">
            <div class="section-heading">
              <div>
                <p class="mini-title">反馈预览</p>
                <h2>{{ submitted ? '今日反馈已生成' : '填写后会在这里展示' }}</h2>
              </div>
              <span class="badge alt">{{ form.className }}</span>
            </div>

            <div class="student-head">
              <div class="avatar-ring">{{ form.studentName.slice(0, 1) }}</div>
              <div>
                <h3>{{ form.studentName }}</h3>
                <p>{{ form.mood }}</p>
              </div>
            </div>

            <div class="summary-list">
              <article v-for="card in summaryCards" :key="card.label">
                <span>{{ card.label }}</span>
                <p>{{ card.value }}</p>
              </article>
            </div>

            <div class="help-box">
              <span>需要帮助</span>
              <p>{{ form.needHelp || '暂时没有需要特别帮助的地方。' }}</p>
            </div>
          </section>
        </div>
      </section>
    </main>
  </div>
</template>
