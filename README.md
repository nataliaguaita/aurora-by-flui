# Aurora by Flui — Protótipo Navegável · Etapa 1

> Protótipo de alta fidelidade do app mobile Aurora by Flui, desenvolvido como entrega da Etapa 1 do Charge Platform Challenge — parceria FIAP, Flui & Google · 2026.

---

## Sobre o projeto

O **Aurora by Flui** é um guia de eletropostos para motoristas de veículos elétricos e híbridos plug-in (EVs e PHEVs) no Brasil. O produto foi concebido como estratégia de captação de leads qualificados para o marketplace de seminovos elétricos da Flui, com potencial de se tornar uma empresa independente no futuro.

O conceito central é o **Guia Michelin aplicado a eletropostos**: não apenas mostrar onde carregar, mas ajudar o motorista a escolher o melhor ponto, com informações detalhadas, avaliações por critério e contexto real de uso.

---

## O que está neste repositório

```
/
├── app.html       → Protótipo navegável do app mobile (motoristas)
├── web.html       → Protótipo navegável da plataforma web (equipe Flui)
└── README.md      → Este arquivo
```

Ambos os arquivos são **100% autocontidos** — sem backend, sem dependências locais, sem build. Basta abrir no navegador.

---

## App Mobile — Aurora by Flui

### Telas implementadas

| # | Tela | Descrição |
|---|------|-----------|
| 1 | **Splash / Onboarding** | Animação de aurora boreal em CSS puro com elétrons flutuantes, apresentação do produto e acesso sem cadastro |
| 2 | **Mapa de pontos** | Mapa fullscreen com pins de status (livre / ocupado / offline), busca flutuante, filter pills e glass card do ponto selecionado |
| 3 | **Ficha detalhada** | Layout bento com status de cada carregador, gráfico de movimento por horário, comodidades e avaliações |
| 4 | **Busca com filtros** | Filtro automático pelo veículo cadastrado, filtros de comodidades e listagem de resultados |
| 5 | **Avaliação — 3 etapas** | Etapa 1: impressão geral (emoji); Etapa 2: critérios detalhados (estilo Michelin); Etapa 3: comentário livre com foto e sistema de créditos |
| 6 | **Planejamento de viagem** | Rota com paradas de recarga calculadas, modo offline, estimativa de bateria por trecho |
| 7 | **Perfil do usuário** | Veículo ativo com specs técnicas, multi-veículo, favoritos e histórico de recargas |

### Diferenciais de UX implementados

- **Filtro por veículo cadastrado** — o usuário cadastra o carro no perfil e o mapa filtra automaticamente os pontos compatíveis, sem precisar conhecer termos técnicos como CCS2 ou CHAdeMO
- **Avaliação progressiva em 3 camadas** — do mais simples (1 emoji, 3 segundos) ao mais completo (critérios + comentário + foto), com créditos proporcionais ao esforço
- **Sistema de créditos visível** — cada ação tem o valor em créditos explícito na interface
- **Aurora boreal animada** — onboarding com gradientes em movimento, elétrons flutuantes e linhas de conexão, tudo em CSS puro sem JavaScript
- **Glass card sobre mapa** — padrão Apple de overlay com backdrop-filter para informação contextual sem abandonar o mapa
- **Navegação com histórico** — botão voltar respeita o fluxo anterior do usuário

### Identidade visual

| Token | Valor | Uso |
|-------|-------|-----|
| `--green` | `#AAFF3E` | Ação primária, status livre, CTAs |
| `--purple` | `#7C3FCC` | Identidade Flui, gradientes |
| `--pl` | `#B87DFF` | Avaliações, estrelas, elementos secundários |
| `--amber` | `#FFB23E` | Status ocupado, atenção |
| `--red` | `#FF5F5F` | Status offline, erro |
| `--base` | `#0A0A0F` | Fundo principal |
| `--surface` | `#13131A` | Cards e superfícies |

**Tipografia:** Sora (títulos, peso 600–800) + DM Sans (corpo, peso 400–500) — ambas gratuitas no Google Fonts.

---

## Plataforma Web — Painel Flui

### Telas implementadas

| # | Tela | Descrição |
|---|------|-----------|
| 1 | **Dashboard** | Métricas da rede, alerta de ponto offline, mini-mapa ao vivo, gráfico de recargas e últimas avaliações |
| 2 | **Listagem de pontos** | Tabela filtrável com status, painel lateral de detalhe com carregadores individuais e ações |
| 3 | **Avaliações** | Nota geral, barras por critério Michelin, histórico de avaliações com chips de nota, distribuição e ranking |
| 4 | **Relatórios** | Métricas mensais, gráfico por semana, heatmap de horários, donut de conectores e top pontos |
| 5 | **Cadastro de ponto** | Formulário com chips interativos de conector e comodidades, mapa com pin ajustável |

---

## Como rodar localmente

Não é necessário instalar nada.

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/aurora-by-flui.git

# Abra os arquivos diretamente no navegador
# macOS
open app.html
open web.html

# Windows
start app.html
start web.html

# Linux
xdg-open app.html
xdg-open web.html
```

Ou simplesmente arraste os arquivos para uma aba do navegador.

---

## Decisões técnicas

### Arquitetura do protótipo

```
Estado global simples
├── cur (string)         → tela atual
├── hist (array)         → histórico para navegação com voltar
└── curStep (number)     → etapa atual na tela de avaliação

Navegação
├── goTo(name)           → transição forward com slide
├── goBack()             → transição backward com slide reverso
└── updateUI()           → sincroniza dots de progresso

Componentes reutilizáveis (CSS)
├── .screen              → container de tela com transição
├── .badge               → status pill com variantes de cor
├── .pin                 → marcador de mapa com cauda
├── .gc (glass card)     → overlay flutuante sobre mapa
├── .bento / .bc         → layout grid modular
└── .nav-bar / .nav-item → navegação inferior
```

### Ícones

Todos os ícones são SVGs inline — sem dependência de CDN ou webfont. Isso garante funcionamento offline e elimina o risco de quebra por mudança de CDN.

### Animação da aurora boreal

Implementada com 3 camadas de `border-radius: 50%` com `filter: blur()` e animações `@keyframes` independentes com durações diferentes (8s, 11s, 14s) para criar movimento orgânico. Elétrons são `position: absolute` com `animation: float`. Linhas de conexão são SVG com `stroke-dashoffset` animado. Zero JavaScript para as animações.

---

## Próximas etapas (Etapa 2+)

- [ ] Backend com API REST (Node.js + Express ou Python + FastAPI)
- [ ] Banco de dados (PostgreSQL) com estrutura para pontos, usuários, avaliações e créditos
- [ ] Migração do app para React Native com Expo
- [ ] Migração da web para React + Vite
- [ ] Integração com Google Maps API para mapa real
- [ ] Sistema de autenticação (Login by Flui — OAuth 2.0)
- [ ] Deploy completo com documentação de endpoints

---

## Integrantes

| Nome | RM |
|------|------|
| Natalia Guaita | RM560106 |
| Patricia Eihara | RM |
| Rafael Santos | RM560567 |

---

## Links

- Protótipo app: https://nataliaguaita.github.io/aurora-by-flui/app.html
- Protótipo web: https://nataliaguaita.github.io/aurora-by-flui/web.html
