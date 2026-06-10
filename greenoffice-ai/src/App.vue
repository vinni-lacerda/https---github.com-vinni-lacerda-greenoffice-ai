<script setup>
import { computed, ref } from 'vue'
import { Bar } from 'vue-chartjs'
import {
  AlertTriangle,
  Bot,
  Droplets,
  FileText,
  Leaf,
  Lightbulb,
  Medal,
  Send,
  Sparkles,
  Trophy,
  Zap,
} from 'lucide-vue-next'
import {
  BarElement,
  CategoryScale,
  Chart as ChartJS,
  Legend,
  LinearScale,
  Tooltip,
} from 'chart.js'

ChartJS.register(CategoryScale, LinearScale, BarElement, Tooltip, Legend)

// Dados mockados do MVP para simular uma dashboard corporativa sustentável.
const indicators = [
  {
    title: 'Energia consumida',
    value: '1.240 kWh',
    note: '+28% em abril',
    icon: Zap,
    tone: 'amber',
  },
  {
    title: 'Água consumida',
    value: '8.500 L',
    note: 'Meta mensal em andamento',
    icon: Droplets,
    tone: 'blue',
  },
  {
    title: 'Papel economizado',
    value: '320 folhas',
    note: '+18% em relação ao mês anterior',
    icon: FileText,
    tone: 'green',
  },
  {
    title: 'Score sustentável',
    value: '82/100',
    note: 'Nivel competitivo saudavel',
    icon: Leaf,
    tone: 'emerald',
  },
]

const monthlyConsumption = {
  labels: ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho'],
  values: [900, 1000, 980, 1240, 1100, 950],
}

const chartData = computed(() => ({
  labels: monthlyConsumption.labels,
  datasets: [
    {
      label: 'Consumo de energia (kWh)',
      data: monthlyConsumption.values,
      backgroundColor: ['#86efac', '#6ee7b7', '#7dd3fc', '#f59e0b', '#34d399', '#22c55e'],
      borderRadius: 8,
      borderSkipped: false,
      maxBarThickness: 52,
    },
  ],
}))

const chartOptions = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    legend: {
      display: false,
    },
    tooltip: {
      backgroundColor: '#0f172a',
      padding: 12,
      titleColor: '#f8fafc',
      bodyColor: '#d1fae5',
      displayColors: false,
    },
  },
  scales: {
    x: {
      grid: {
        display: false,
      },
      ticks: {
        color: '#64748b',
        font: {
          size: 12,
          weight: 600,
        },
      },
    },
    y: {
      beginAtZero: true,
      grid: {
        color: '#e2e8f0',
      },
      ticks: {
        color: '#64748b',
        callback: (value) => `${value} kWh`,
      },
    },
  },
}

const alerts = [
  'O consumo de energia subiu 28% em abril. Verifique equipamentos ligados fora do expediente.',
  'O setor Administrativo teve aumento no uso de papel. Recomenda-se priorizar documentos digitais.',
  'Consumo de água fora do padrão detectado. Possível vazamento ou uso excessivo.',
]

const ranking = [
  { sector: 'RH', score: 92 },
  { sector: 'TI', score: 85 },
  { sector: 'Financeiro', score: 76 },
  { sector: 'Administrativo', score: 68 },
]

const impacts = [
  'Redução de custos operacionais',
  'Menor impacto ambiental',
  'Apoio a metas ESG',
  'Melhoria da imagem da empresa',
  'Engajamento dos colaboradores',
]

const question = ref('')
const assistantReply = ref(
  'Posso ajudar com sugestões sobre água, energia, papel e práticas sustentáveis no escritório.',
)

function askAssistant() {
  const text = question.value.toLowerCase()

  if (text.includes('agua') || text.includes('água') || text.includes('vazamento')) {
    assistantReply.value =
      'Para reduzir o consumo de água, recomenda-se instalar arejadores, verificar vazamentos e reutilizar água sempre que possível.'
  } else if (text.includes('energia') || text.includes('luz') || text.includes('kwh')) {
    assistantReply.value =
      'Para reduzir energia, desligue equipamentos fora do expediente, use sensores de presença e substitua lâmpadas por LED.'
  } else if (text.includes('papel') || text.includes('impressao') || text.includes('documento')) {
    assistantReply.value =
      'Para economizar papel, priorize documentos digitais, impressão frente e verso e assinatura eletrônica.'
  } else {
    assistantReply.value =
      'Posso ajudar com sugestões sobre água, energia, papel e práticas sustentáveis no escritório.'
  }

  question.value = ''
}
</script>

<template>
  <main class="app-shell">
    <section class="hero-section">
      <div class="hero-copy">
        <span class="eyebrow"><Sparkles :size="16" /> MVP de hackathon sustentável</span>
        <h1>GreenOffice AI</h1>
        <p class="subtitle">Dashboard inteligente para sustentabilidade empresarial</p>
        <p class="description">
          A solução ajuda empresas a reduzirem desperdícios de energia, água e papel com
          indicadores, alertas inteligentes e recomendações práticas para decisão rápida.
        </p>
      </div>

      <div class="hero-panel" aria-label="Resumo de sustentabilidade">
        <Leaf :size="34" />
        <strong>82</strong>
        <span>score sustentável atual</span>
      </div>
    </section>

    <section class="indicator-grid" aria-label="Indicadores principais">
      <article
        v-for="indicator in indicators"
        :key="indicator.title"
        class="metric-card"
        :class="`tone-${indicator.tone}`"
      >
        <div class="metric-icon">
          <component :is="indicator.icon" :size="22" />
        </div>
        <div>
          <h2>{{ indicator.title }}</h2>
          <strong>{{ indicator.value }}</strong>
          <p>{{ indicator.note }}</p>
        </div>
      </article>
    </section>

    <section class="dashboard-grid">
      <article class="panel chart-panel">
        <div class="section-heading">
          <div>
            <span>Consumo mensal</span>
            <h2>Evolução do consumo de energia</h2>
          </div>
          <Lightbulb :size="24" />
        </div>
        <div class="chart-wrap">
          <Bar :data="chartData" :options="chartOptions" />
        </div>
      </article>

      <article class="panel">
        <div class="section-heading">
          <div>
            <span>Alertas Inteligentes</span>
            <h2>Sugestões geradas por IA</h2>
          </div>
          <AlertTriangle :size="24" />
        </div>
        <ul class="alerts-list">
          <li v-for="alert in alerts" :key="alert">
            <Bot :size="18" />
            <span>{{ alert }}</span>
          </li>
        </ul>
      </article>
    </section>

    <section class="dashboard-grid lower-grid">
      <article class="panel">
        <div class="section-heading">
          <div>
            <span>Ranking sustentável por setor</span>
            <h2>Gamificação interna</h2>
          </div>
          <Trophy :size="24" />
        </div>
        <ol class="ranking-list">
          <li v-for="(item, index) in ranking" :key="item.sector">
            <span class="position">{{ index + 1 }}o</span>
            <div>
              <strong>{{ item.sector }}</strong>
              <div class="score-track">
                <span :style="{ width: `${item.score}%` }"></span>
              </div>
            </div>
            <strong>{{ item.score }} pontos</strong>
          </li>
        </ol>
      </article>

      <article class="panel assistant-panel">
        <div class="section-heading">
          <div>
            <span>Assistente Sustentável</span>
            <h2>Chatbot de recomendações</h2>
          </div>
          <Bot :size="24" />
        </div>

        <div class="chat-box">
          <div class="assistant-avatar">
            <Leaf :size="20" />
          </div>
          <p>{{ assistantReply }}</p>
        </div>

        <form class="chat-form" @submit.prevent="askAssistant">
          <input
            v-model="question"
            type="text"
            placeholder="Pergunte sobre água, energia ou papel"
            aria-label="Pergunta para o assistente sustentável"
          />
          <button type="submit">
            <Send :size="18" />
            Perguntar
          </button>
        </form>
      </article>
    </section>

    <section class="impact-section">
      <div class="section-heading">
        <div>
          <span>Impacto esperado</span>
          <h2>Benefícios para empresas</h2>
        </div>
        <Medal :size="24" />
      </div>
      <div class="impact-grid">
        <article v-for="impact in impacts" :key="impact">
          <Leaf :size="18" />
          <span>{{ impact }}</span>
        </article>
      </div>
    </section>
  </main>
</template>

<style scoped>
:global(*) {
  box-sizing: border-box;
}

:global(body) {
  margin: 0;
  background: #edf7f0;
  color: #10231a;
  font-family:
    Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

:global(button),
:global(input) {
  font: inherit;
}

.app-shell {
  min-height: 100vh;
  padding: 28px;
  background:
    radial-gradient(circle at 12% 4%, rgba(34, 197, 94, 0.14), transparent 26%),
    linear-gradient(135deg, #f8fff9 0%, #eef9f3 48%, #f4fbff 100%);
}

.hero-section,
.dashboard-grid,
.impact-section {
  width: min(1180px, 100%);
  margin: 0 auto;
}

.hero-section {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 280px;
  gap: 24px;
  align-items: stretch;
  padding: 32px;
  border: 1px solid rgba(22, 101, 52, 0.14);
  border-radius: 22px;
  background:
    linear-gradient(120deg, rgba(255, 255, 255, 0.96), rgba(236, 253, 245, 0.9)),
    linear-gradient(90deg, rgba(21, 128, 61, 0.08), transparent);
  box-shadow: 0 20px 60px rgba(15, 118, 110, 0.12);
}

.hero-copy {
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-width: 0;
}

.eyebrow {
  display: inline-flex;
  width: fit-content;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  border-radius: 999px;
  background: #dcfce7;
  color: #166534;
  font-size: 0.82rem;
  font-weight: 800;
  text-transform: uppercase;
}

h1,
h2,
p {
  margin: 0;
}

h1 {
  margin-top: 18px;
  color: #0f3d25;
  font-size: clamp(2.7rem, 6vw, 5.5rem);
  line-height: 0.96;
}

.subtitle {
  margin-top: 14px;
  color: #15803d;
  font-size: clamp(1.1rem, 2.2vw, 1.55rem);
  font-weight: 800;
}

.description {
  max-width: 760px;
  margin-top: 12px;
  color: #475569;
  font-size: 1.02rem;
  line-height: 1.7;
}

.hero-panel {
  display: grid;
  place-items: center;
  align-content: center;
  gap: 8px;
  min-height: 240px;
  border-radius: 18px;
  background: #0f3d25;
  color: #ecfdf5;
  text-align: center;
}

.hero-panel strong {
  font-size: 4.6rem;
  line-height: 1;
}

.hero-panel span {
  color: #bbf7d0;
  font-weight: 700;
}

.indicator-grid {
  display: grid;
  width: min(1180px, 100%);
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 16px;
  margin: 18px auto;
}

.metric-card,
.panel,
.impact-section {
  border: 1px solid rgba(22, 101, 52, 0.12);
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.86);
  box-shadow: 0 16px 42px rgba(15, 23, 42, 0.08);
}

.metric-card {
  display: flex;
  gap: 14px;
  min-height: 146px;
  padding: 18px;
}

.metric-icon {
  display: grid;
  flex: 0 0 46px;
  width: 46px;
  height: 46px;
  place-items: center;
  border-radius: 14px;
  background: #dcfce7;
  color: #166534;
}

.metric-card h2 {
  color: #64748b;
  font-size: 0.9rem;
  font-weight: 800;
}

.metric-card strong {
  display: block;
  margin-top: 8px;
  color: #0f172a;
  font-size: 1.75rem;
  line-height: 1;
}

.metric-card p {
  margin-top: 10px;
  color: #64748b;
  font-size: 0.9rem;
}

.tone-amber .metric-icon {
  background: #fef3c7;
  color: #b45309;
}

.tone-blue .metric-icon {
  background: #dbeafe;
  color: #0369a1;
}

.tone-green .metric-icon {
  background: #dcfce7;
  color: #15803d;
}

.tone-emerald .metric-icon {
  background: #ccfbf1;
  color: #0f766e;
}

.dashboard-grid {
  display: grid;
  grid-template-columns: minmax(0, 1.35fr) minmax(320px, 0.75fr);
  gap: 18px;
  margin-top: 18px;
}

.lower-grid {
  grid-template-columns: minmax(320px, 0.85fr) minmax(0, 1.15fr);
}

.panel,
.impact-section {
  padding: 22px;
}

.section-heading {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  color: #15803d;
}

.section-heading span {
  display: block;
  color: #16a34a;
  font-size: 0.78rem;
  font-weight: 900;
  letter-spacing: 0;
  text-transform: uppercase;
}

.section-heading h2 {
  margin-top: 6px;
  color: #10231a;
  font-size: 1.35rem;
}

.chart-wrap {
  height: 320px;
  margin-top: 22px;
}

.alerts-list,
.ranking-list {
  display: grid;
  gap: 12px;
  margin: 20px 0 0;
  padding: 0;
  list-style: none;
}

.alerts-list li {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  padding: 14px;
  border-radius: 14px;
  background: #f8fafc;
  color: #334155;
  line-height: 1.5;
}

.alerts-list svg {
  flex: 0 0 auto;
  margin-top: 2px;
  color: #15803d;
}

.ranking-list li {
  display: grid;
  grid-template-columns: 44px minmax(0, 1fr) auto;
  gap: 12px;
  align-items: center;
  padding: 13px 0;
  border-bottom: 1px solid #e2e8f0;
}

.ranking-list li:last-child {
  border-bottom: 0;
}

.position {
  display: grid;
  width: 38px;
  height: 38px;
  place-items: center;
  border-radius: 50%;
  background: #dcfce7;
  color: #166534;
  font-weight: 900;
}

.score-track {
  height: 8px;
  margin-top: 8px;
  overflow: hidden;
  border-radius: 999px;
  background: #e2e8f0;
}

.score-track span {
  display: block;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(90deg, #22c55e, #14b8a6);
}

.assistant-panel {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.chat-box {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  padding: 16px;
  border-radius: 16px;
  background: #f0fdf4;
  color: #14532d;
  line-height: 1.6;
}

.assistant-avatar {
  display: grid;
  flex: 0 0 38px;
  width: 38px;
  height: 38px;
  place-items: center;
  border-radius: 50%;
  background: #166534;
  color: #dcfce7;
}

.chat-form {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  gap: 10px;
}

.chat-form input {
  min-width: 0;
  padding: 14px 16px;
  border: 1px solid #bbf7d0;
  border-radius: 14px;
  background: #ffffff;
  color: #0f172a;
  outline: none;
}

.chat-form input:focus {
  border-color: #22c55e;
  box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.14);
}

.chat-form button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 0 18px;
  border: 0;
  border-radius: 14px;
  background: #15803d;
  color: #ffffff;
  font-weight: 900;
  cursor: pointer;
  transition:
    transform 0.2s ease,
    background 0.2s ease;
}

.chat-form button:hover {
  background: #166534;
  transform: translateY(-1px);
}

.impact-section {
  margin-top: 18px;
}

.impact-grid {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 12px;
  margin-top: 18px;
}

.impact-grid article {
  display: flex;
  min-height: 86px;
  align-items: center;
  gap: 10px;
  padding: 14px;
  border-radius: 14px;
  background: #f8fafc;
  color: #334155;
  font-weight: 800;
}

.impact-grid svg {
  flex: 0 0 auto;
  color: #16a34a;
}

@media (max-width: 980px) {
  .app-shell {
    padding: 18px;
  }

  .hero-section,
  .dashboard-grid,
  .lower-grid {
    grid-template-columns: 1fr;
  }

  .indicator-grid,
  .impact-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .hero-panel {
    min-height: 180px;
  }
}

@media (max-width: 620px) {
  .hero-section,
  .panel,
  .impact-section {
    padding: 18px;
    border-radius: 16px;
  }

  .indicator-grid,
  .impact-grid {
    grid-template-columns: 1fr;
  }

  .chat-form,
  .ranking-list li {
    grid-template-columns: 1fr;
  }

  .chat-form button {
    min-height: 48px;
  }
}
</style>
