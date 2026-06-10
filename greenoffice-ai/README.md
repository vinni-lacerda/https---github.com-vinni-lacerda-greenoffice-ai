# GreenOffice AI

Protótipo funcional de uma dashboard inteligente para sustentabilidade empresarial, criado para a disciplina **Inovação, Sustentabilidade e Competitividade Empresarial**.

O projeto simula uma solução desenvolvida em um hackathon de soluções sustentáveis. A proposta é ajudar empresas a monitorarem consumo de recursos, identificarem desperdícios e engajarem setores internos em práticas mais sustentáveis.

## Objetivo

O **GreenOffice AI** apresenta indicadores, alertas simulados por IA e recomendações práticas para apoiar decisões rápidas sobre consumo de energia, água e papel em ambientes corporativos.

Este é um MVP visual e funcional, sem backend, banco de dados, autenticação ou API real. Todos os dados são mockados diretamente no front-end.

## Funcionalidades

- Dashboard principal com identidade visual sustentável e tecnológica.
- Cards de indicadores:
  - Energia consumida: `1.240 kWh`
  - Água consumida: `8.500 L`
  - Papel economizado: `320 folhas`
  - Score sustentável: `82/100`
- Gráfico de consumo mensal com dados simulados dos últimos meses.
- Alertas inteligentes com recomendações de economia.
- Ranking sustentável por setor para simular gamificação interna.
- Assistente sustentável fake com respostas pré-programadas sobre água, energia e papel.
- Seção final com benefícios da solução para empresas.
- Layout responsivo para notebook, projetor e telas menores.

## Tecnologias

- Vue 3
- Vite
- JavaScript
- CSS puro
- Chart.js
- vue-chartjs
- lucide-vue-next

## Como Rodar

Entre na pasta do projeto:

```bash
cd greenoffice-ai
```

Instale as dependências:

```bash
npm install
```

Inicie o servidor de desenvolvimento:

```bash
npm run dev
```

Acesse no navegador:

```text
http://localhost:5173
```

## Build de Produção

Para gerar a versão final:

```bash
npm run build
```

Para visualizar o build localmente:

```bash
npm run preview
```

## Roteiro Rápido de Demonstração

1. Apresentar o problema: empresas desperdiçam energia, água e papel por falta de monitoramento simples.
2. Mostrar os cards principais da dashboard.
3. Explicar o gráfico de consumo mensal e o pico de abril.
4. Demonstrar os alertas inteligentes como sugestões simuladas por IA.
5. Mostrar o ranking por setor como mecanismo de gamificação.
6. Testar o assistente sustentável com perguntas sobre `água`, `energia` ou `papel`.
7. Encerrar com a seção de impacto e benefícios para metas ESG.

## Observação

Este projeto é um protótipo acadêmico. A inteligência artificial, os dados de consumo e os alertas são simulados para fins de apresentação.
