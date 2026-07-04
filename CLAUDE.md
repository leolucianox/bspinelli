# Landing Page — Dra. Beatriz Spinelli (Harmonização Facial)

Landing page estática de página única para a Dra. Beatriz Spinelli (harmonização facial, CROSP 162964, atendimento em São José dos Campos e Caraguatatuba).

## Stack

- **HTML puro + Tailwind CSS via Play CDN** (`<script src="https://cdn.tailwindcss.com">` no `<head>`).
- **Sem build step, sem npm, sem `package.json`.** Não é um projeto Next.js/React — é um único arquivo `index.html` autossuficiente.
- Fontes via Google Fonts: Hanken Grotesk (sans) e Cormorant Garamond (serif).
- Tema Tailwind (cores/fontes customizadas) configurado inline em `<script>tailwind.config = {...}</script>` no próprio `index.html`.

## Estrutura

```
index.html          → página inteira (nav, hero, seções, footer)
assets/img/*.png    → fotos usadas no site (as únicas que importam pro deploy)
refs/*.png          → fotos brutas de referência do cliente (gitignored, não vai pro deploy)
.gitignore          → ignora refs/ e uploads/
```

## Rodar localmente

Não precisa de servidor nem build: abra `index.html` direto no navegador, ou sirva a pasta com qualquer static server (`npx serve`, extensão Live Server, etc.).

## Pendência conhecida

O número de WhatsApp está com **placeholder** (`5512999999999`) em 7 lugares (nav, hero, box de contato, CTA final, footer, botão flutuante, menu mobile), cada um marcado com o comentário `<!-- TROCAR: numero do WhatsApp -->`. Buscar por `TROCAR` ou `5512999999999` no `index.html` antes de considerar o site "no ar" de verdade.

## Deploy (Vercel)

Site 100% estático — **não existe framework, não existe versão de Next/React pra dar conflito**. Ao importar o repo no Vercel:

- Framework Preset: **Other** (ou "No Framework Detected")
- Build Command: deixar vazio
- Output Directory: `./` (raiz)

Nenhuma dependência para instalar, nenhum `next.config`/`package.json` — o erro clássico de "versão do Next" não se aplica aqui porque não há Next.js no projeto.

## Responsividade

Testado e ajustado nos breakpoints: mobile 375/390px, tablet 768px, desktop 1280/1440px, usando classes responsivas do Tailwind (`sm:` `md:` `lg:` `xl:`). Menu mobile é um hambúrguer (`<768px`); nav completa aparece a partir de `md:` (768px). Grids fazem reflow 1→2→3 colunas conforme a seção.

## Comportamentos JS (vanilla, sem dependências)

Todo o JS fica em `<script>` inline no fim do `index.html`:
- Toggle do menu hambúrguer mobile.
- Navbar (`#site-header`, `position: sticky`) some ao rolar pra baixo e reaparece ao rolar pra cima, em qualquer ponto da página.
- Scrollbar lateral escondida via CSS (`scrollbar-width: none` / `::-webkit-scrollbar { display: none }`), scroll continua funcionando normalmente.

**Atenção:** o `overflow-x-hidden` precisa ficar no `<body>`, não em uma `<div>` interna — colocá-lo numa div ancestral do header quebra o cálculo de `position: sticky` em navegadores reais (bug já corrigido uma vez neste projeto).
