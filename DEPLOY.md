# Deploy

Instruções para publicar o blog no GitHub Pages ou Cloudflare Pages.

---

## GitHub Pages

### 1. Criar o repositório

Crie um repositório público no GitHub. Para o site ficar em `seuusuario.github.io`, o nome do repositório deve ser exatamente `seuusuario.github.io`.

Para qualquer outro nome, o site fica em `seuusuario.github.io/nome-do-repo`.

### 2. Enviar os arquivos

```bash
git init
git add .
git commit -m "init"
git remote add origin https://github.com/seuusuario/nome-do-repo.git
git push -u origin main
```

### 3. Ativar o GitHub Pages

No repositório, acesse **Settings → Pages**. Em **Source**, selecione a branch `main` e a pasta `/ (root)`. Salve.

O site estará disponível em alguns minutos.

### 4. SPA e o 404.html

O GitHub Pages não redireciona rotas desconhecidas para o `index.html`. O `404.html` incluído no projeto resolve isso — o GitHub Pages serve esse arquivo para qualquer rota não encontrada e o router assume o controle.

### 5. Atenção: ES Modules e paths

Se o repositório não for `seuusuario.github.io` mas sim `seuusuario.github.io/nome-do-repo`, os paths relativos do `config.js` continuam funcionando normalmente pois são relativos ao `index.html`.

---

## Cloudflare Pages

### 1. Acessar o dashboard

Acesse [pages.cloudflare.com](https://pages.cloudflare.com) e faça login.

### 2. Criar o projeto

Clique em **Create a project → Connect to Git**. Autorize o acesso ao GitHub e selecione o repositório.

### 3. Configurar o build

O projeto não tem build step. Configure assim:

| Campo | Valor |
|---|---|
| Framework preset | None |
| Build command | *(vazio)* |
| Build output directory | `/` |

Clique em **Save and Deploy**.

### 4. SPA no Cloudflare Pages

O Cloudflare Pages suporta SPAs nativamente quando há um `404.html` na raiz, sem configuração adicional.

---

## Atualizar o blog

Para publicar um novo post ou atualizar qualquer arquivo:

```bash
git add .
git commit -m "novo post: título"
git push
```

O deploy atualiza automaticamente em ambas as plataformas.

---

## Observações

- A pasta `posts/` com os arquivos `.md` deve estar incluída no repositório.
- A pasta `data/` com o `posts.json` deve estar incluída no repositório.
- O `marked.min.js` em `src/` deve estar incluído no repositório — não há CDN externo.