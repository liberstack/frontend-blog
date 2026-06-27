# liberstack/blog

Blog estático com HTML, CSS e JavaScript vanilla. Sem frameworks, sem build step, sem dependências além do marked.js para renderização de posts em Markdown.

## Stack

- HTML, CSS e JavaScript vanilla (ES Modules)
- marked.js para renderização de posts Markdown
- Deploy via GitHub Pages ou Cloudflare Pages

## Estrutura

```
config/
  config.js         ← nome do site, nav, paths
data/
  posts.json        ← índice dos posts (título, slug, data, excerpt, tag)
pages/
  home.html         ← fragmento da home (search + lista de posts)
  about.html        ← fragmento da página sobre
  contact.html      ← fragmento da página contato
  legal.html        ← fragmento da página legal
posts/
  *.md              ← conteúdo dos posts em Markdown
src/
  app.js            ← ponto de entrada (ES Module)
  router.js         ← hash router com suporte a parâmetros (/p/:slug)
  ui.js             ← renderização de navbar, footer e conteúdo
404.html            ← fallback para GitHub Pages
index.html          ← shell do blog
style.css           ← visual completo
```

## Arquitetura

O `index.html` é o shell fixo. O `router.js` escuta mudanças de hash e despacha para o handler correto. O `ui.js` faz fetch dos fragmentos HTML de `pages/` e injeta no `#app`. Os posts são carregados a partir do índice `data/posts.json` e o conteúdo `.md` é renderizado via marked.js.

O `config.js` é um ES Module exportado com `export default` — centraliza nome do site, autor, nav e paths.

## Como adicionar um post

**1. Criar o arquivo Markdown:**

```
posts/meu-post.md
```

**2. Registrar no índice:**

```json
{
  "slug": "meu-post",
  "title": "Título do post",
  "date": "2026-06-27",
  "excerpt": "Resumo curto que aparece na listagem.",
  "tag": "javascript",
  "file": "meu-post.md"
}
```

O post aparece automaticamente na home com search e ordenação por data.

## Como adicionar uma página

**1. Criar o fragmento em `pages/`:**

```html
<!-- pages/projetos.html -->
<div class="page-header">
  <h1>Projetos</h1>
</div>
<p>Conteúdo da página.</p>
```

**2. Registrar a rota no `app.js`:**

```js
router.register("/projetos", () => loadPage("projetos"));
```

**3. Adicionar na nav do `config.js`:**

```js
{ label: "projetos", href: "#/projetos" }
```

## Como rodar localmente

Requer um servidor local — ES Modules não funcionam via `file://`.

Com VS Code, use a extensão Live Server. Pela linha de comando:

```bash
npx serve .
```

## Deploy

Veja o [DEPLOY.md](./DEPLOY.md).