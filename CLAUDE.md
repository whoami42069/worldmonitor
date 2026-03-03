# World Monitor — Turkish War Edition

## Project Overview
Personal fork of worldmonitor focused on Middle East war coverage. Stripped non-war content (tech, AI, layoffs panels), removed original branding, added DÜNYA / ORTA DOĞU header tabs with a dedicated Middle East War News panel featuring auto-translation to Turkish via Google Translate.

## Stack
- **Frontend:** TypeScript, Vanilla JS (no framework), Vite bundler
- **Map:** DeckGL + MapLibre GL JS
- **Styling:** CSS custom properties (dark/light theme), responsive grid
- **Backend:** Vercel serverless functions (Node.js)
- **AI:** DeepSeek via Ollama (self-hosted), Groq, OpenRouter
- **Caching:** Upstash Redis, IndexedDB (client-side)
- **Deployment:** Vercel

## Branch
- `turkish-edition` (based on `main`)
- Repo: `whoami42069/worldmonitor`

## Key Files
| File | Purpose |
|------|---------|
| `src/config/panels.ts` | Panel definitions per variant (FULL_PANELS), map layers, category map |
| `src/config/feeds.ts` | RSS feed URLs, source tiers, propaganda risk, region map |
| `src/app/panel-layout.ts` | Main layout: header, variant tabs, panel grid, map section |
| `src/app/data-loader.ts` | Data orchestration: news fetching, clustering, market data, Middle East filter |
| `src/components/InsightsPanel.ts` | AI analysis: keyword scoring, cluster ranking, drill-down UI |
| `src/components/Panel.ts` | Base panel class: resize handles, drag, localStorage persistence |
| `src/components/NewsPanel.ts` | News rendering: flat list + clustered view, translate button |
| `src/components/UnifiedSettings.ts` | Settings modal: panels, sources, AI providers, font size |
| `server/worldmonitor/news/v1/_shared.ts` | Summarization prompts, provider credentials (Ollama, Groq, OpenRouter) |
| `src/styles/main.css` | All CSS: themes, components, responsive, animations |

## Turkish War Edition Changes
- Disabled panels: `tech`, `ai`, `layoffs`, `world-clock`
- Added panel: `mideast-war` (Orta Doğu Savaş Haberleri)
- Header: DÜNYA + ORTA DOĞU tabs replace variant switcher
- Removed: Twitter credit, GitHub link, CommunityWidget
- AI: Removed `think: false` from Ollama config
- Dashboard: Panel font size setting (S/M/L), map un-pinned
- InsightsPanel: Click-to-expand drill-down with source URLs
- Focal points: Expandable with all headlines and signal types
- Translation: Google Translate API for non-Turkish headlines (cached, rate-limited)

## Environment Variables (Vercel)
- `UPSTASH_REDIS_REST_URL` — Redis cache endpoint
- `UPSTASH_REDIS_REST_TOKEN` — Redis auth token
- `OLLAMA_API_URL` — DeepSeek/Ollama endpoint
- `OLLAMA_MODEL` — Model name (default: llama3.1:8b)
- `GROQ_API_KEY` — Groq API key (optional)

## Build
```bash
npm install
npm run build          # Production build
npm run dev            # Dev server
npx tsc --noEmit       # Type check only
```

## Conventions
- No React/Vue — vanilla TypeScript with DOM manipulation
- Panel system: extend `Panel` base class, register in `panel-layout.ts`
- News items: `NewsItem` type with `title`, `link`, `pubDate`, `source`, `threat`
- Clustering: `ClusteredEvent` with `topSources[]`, `allItems[]`, `velocity`
- i18n: `t('key')` function, translations in `src/locales/`
- Sanitization: Always use `escapeHtml()` and `sanitizeUrl()` from `@/utils/sanitize`
