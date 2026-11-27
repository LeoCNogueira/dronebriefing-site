# Site do Drone Briefing: como publicar

Site estático para o GitHub Pages, no mesmo esquema dos outros apps Raven, no endereço
**https://dronebriefing.ravendronevideos.com.br**. Os endereços `privacy.html` e `support.html` (e as versões em
`en/`) são os que vão no App Store Connect; a tela de compra do app já aponta para `privacy.html`.

O site não tem cookies, anúncios nem medição. A tag do Google Ads dos outros sites **não** foi colocada; se quiser
usá-la, ela precisa entrar também no texto "Este site" das duas páginas de privacidade.

## O que há na pasta

| Arquivo | Para quê |
|---|---|
| `index.html`, `en/index.html` | Landing page em português e em inglês |
| `support.html`, `privacy.html` (e em `en/`) | Suporte e política de privacidade |
| `404.html` | Página para endereços inexistentes |
| `style.css` | Visual de todas as páginas, com modo claro e escuro |
| `sitemap.xml`, `robots.txt` | Para o Google |
| `CNAME` | O subdomínio do GitHub Pages |
| `.nojekyll` | Arquivo oculto: faz o GitHub Pages publicar os arquivos como estão |
| `assets/` | Ícones do app (64, 180, 256 e 512 px) e `screens/`, as telas do app em JPEG (pt e en) |

## 1. Crie o repositório público

1. No GitHub, crie o repositório **público** `LeoCNogueira/dronebriefing` (o do app, `DroneRadar-app`, continua
   privado). O Pages gratuito exige repositório público.
2. Copie o conteúdo desta pasta para a raiz dele. O `.nojekyll` é oculto no Finder; pelo Terminal:
   ```
   cp -R ~/Developer/DroneRadar-app/site/. ~/Developer/dronebriefing-site/
   ```
3. Commit e push. Em **Settings ▸ Pages**: Source "Deploy from a branch", branch `main`, pasta `/ (root)`.
   O campo Custom domain é preenchido sozinho pelo `CNAME`.

## 2. Aponte o subdomínio

No painel de DNS do `ravendronevideos.com.br`, crie o registro:

| Tipo | Nome | Valor |
|---|---|---|
| CNAME | `dronebriefing` | `leocnogueira.github.io` |

Espere o DNS propagar (minutos a algumas horas) e marque **Enforce HTTPS** em Settings ▸ Pages.

## 3. Antes do lançamento: link e selo da App Store

- Feito: os links da App Store em `index.html` e `en/index.html` (e o `downloadUrl` do JSON-LD) usam o Apple ID
  do app, **6838916058** (`https://apps.apple.com/app/id6838916058`).
- Selos oficiais, sem modificações, do App Store Marketing Tools: **"Baixar na App Store"** (português, preto, SVG)
  em `assets/badge-app-store-pt.svg` e **"Download on the App Store"** (inglês EUA, preto, SVG) em
  `assets/badge-app-store-en.svg`. Sem os arquivos, a página mostra um botão de texto.
- Quando as capturas da loja estiverem prontas, dá para acrescentar uma seção "Veja o app por dentro".

## 4. Ligue o site à loja e ao Google

- **App Store Connect, página em português:** URL de suporte `…/support.html`, URL de marketing `…/`,
  política de privacidade `…/privacy.html`.
- **Página em inglês (U.S.):** `…/en/support.html`, `…/en/` e `…/en/privacy.html`.
- **Google Search Console:** propriedade "Prefixo do URL" `https://dronebriefing.ravendronevideos.com.br/`,
  verificada pelo arquivo HTML do Google na raiz; envie o `sitemap.xml`.

## 5. Confira depois de publicar

- https://dronebriefing.ravendronevideos.com.br/ e `/en/`
- `/privacy.html`, `/support.html`, `/en/privacy.html`, `/en/support.html`
- Um endereço qualquer inexistente deve mostrar a página "Fora da rota".

## Manutenção

- **O site publicado está no repositório público `LeoCNogueira/dronebriefing-site`**; esta pasta é a cópia de
  trabalho. Mude aqui e copie para lá (ou o contrário), para as duas não se separarem.
- **Recursos anunciados antes de sair:** os recursos dos EUA da 1.2 (M10) estão no site desde 27/11/2026 com o
  selo `selo-breve` ("Coming in 1.2" / "Na versão 1.2") e as marcas "from 1.2" / "na 1.2" no texto. **No dia em
  que a Apple aprovar a 1.2, tire os selos e essas marcas** em `index.html`, `en/index.html`, `support.html`,
  `en/support.html` e no cartão do Drone Briefing do site dos apps Raven (`LeoCNogueira/raven-apps`).

- As telas em `assets/screens/` saem do simulador no modo de demonstração (piloto e semana fictícios), em JPEG de
  900 px. Para refazer: capturas com `-demo YES -pro lifetime` e `sips -s format jpeg -s formatOptions 78 -Z 900`.

- Preços (R$ 59,90 por ano e R$ 149,90 vitalício) estão no `index.html`, no quadro de planos e no JSON-LD. Se
  mudarem no App Store Connect, mude aqui também. A página em inglês não mostra preço.
- A política de privacidade lista os serviços que o app consulta. Se o app passar a consultar outro (por exemplo,
  o espaço aéreo do DECEA), atualize as duas versões e a data.
