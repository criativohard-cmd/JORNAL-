# +250 Jornais Biológicos — Página de Vendas

Landing page de vendas (frontend estático) para a coleção de Jornais Biológicos.

## Pacote ZIP do site

- O ZIP contém o código React completo, imagens locais, dependências declaradas, `yarn.lock` e configurações.
- `frontend/public/index.html` é o HTML de entrada do React: **ele não funciona sozinho**. Os componentes e imagens também são necessários.
- No pacote exportado, `frontend/.env.example` contém somente os três links públicos de checkout já configurados. Copie esse arquivo para `frontend/.env` antes de executar ou compilar o projeto.
- Credenciais privadas, backend não utilizado, `node_modules` e arquivos internos de desenvolvimento não fazem parte do pacote. Instale as dependências com `yarn install`.
- O `vercel.json` da raiz acompanha a estrutura completa do ZIP; não mova apenas os três arquivos para uma pasta vazia.

## Stack

- **NÃO é Next.js** — é **React 19 com Create React App** (react-scripts 5)
- Tailwind CSS 3 + framer-motion + lenis + react-fast-marquee
- A pasta `backend/` (FastAPI) não é usada pela página de vendas — o deploy na Vercel usa **apenas o frontend**

## Deploy na Vercel

### Opção A — importar o repositório inteiro (recomendado)
1. Em vercel.com: **Add New → Project** e importe o repositório do GitHub
2. O arquivo `vercel.json` da raiz já configura tudo automaticamente
3. Se a Vercel pedir para confirmar:
   - **Framework Preset:** Create React App
   - **Root Directory:** `./` (raiz)
   - **Build Command:** `yarn --cwd frontend build`
   - **Output Directory:** `frontend/build`
   - **Install Command:** `yarn --cwd frontend install`

### Opção B — apontar direto para a pasta frontend
1. **Root Directory:** `frontend`
2. **Framework Preset:** Create React App
3. **Build Command:** `yarn build` · **Output Directory:** `build` · **Install Command:** `yarn install`

### Variáveis de ambiente (obrigatórias nos dois casos)
Em **Project Settings → Environment Variables**, adicione:

| Nome | Valor |
|---|---|
| `REACT_APP_CHECKOUT_URL` | link do checkout da Coleção Completa (R$ 19,90) |
| `REACT_APP_CHECKOUT_URL_BASIC` | link do checkout do Plano Básico (R$ 10,00) |
| `REACT_APP_CHECKOUT_URL_PRO` | link do checkout do Plano Pro do upsell (R$ 15,00) |

(Os valores atuais estão em `frontend/.env`, que não sobe para o GitHub por segurança.)

## Subir para o GitHub

Use o botão **Save to GitHub** do Emergent, ou manualmente:

```bash
git init
git add .
git commit -m "Página de vendas Jornais Biológicos"
git remote add origin https://github.com/SEU-USUARIO/SEU-REPO.git
git push -u origin main
```

O `.gitignore` já exclui `node_modules`, builds e todos os arquivos `.env` (suas chaves não vazam).

## Rodar localmente

```bash
cd frontend
yarn install
cp .env.example .env   # no ZIP, inclui os 3 links públicos de checkout
yarn start             # http://localhost:3000
yarn build             # gera frontend/build (pasta publicada na Vercel)
```
