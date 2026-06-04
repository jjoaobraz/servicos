# ~/portifolio.sh

Portfólio pessoal com estética de catálogo de serviços — cards com mockups visuais, integração com GitHub e deploy automático no GitHub Pages.

![preview](https://jjoaobraz.github.io/portifolio.sh)

## 🔗 Demo

**[jjoaobraz.github.io/portifolio.sh](https://jjoaobraz.github.io/portifolio.sh)**

---

## 🛠 Stack

| Tech | Uso |
|---|---|
| HTML + CSS + JS puro | Sem framework, zero dependências |
| GitHub Actions | Deploy automático + atualização do WakaTime |
| GitHub Pages | Hospedagem gratuita |
| GitHub API | Dados públicos do perfil em tempo real |
| WakaTime API | Horas de código na semana (opcional) |

---

## ✨ Features

- **Cards de serviços** com mockups visuais (browser, dashboard, terminal, WhatsApp, tabela SQL)
- **Botões WhatsApp** com mensagem pré-preenchida por serviço
- **Foto via GitHub** — avatar puxado direto de `github.com/<username>.png`
- **GitHub API** — repos e seguidores em tempo real (sem token necessário)
- **WakaTime** — horas codando na semana via GitHub Action agendado
- **Deploy automático** — qualquer push na `main` publica o site
- **100% responsivo** — mobile e desktop
- **Zero dependências** — sem npm, sem build, sem framework

---

## 🚀 Como usar

### 1. Fork ou clone o repositório

```bash
git clone https://github.com/jjoaobraz/portifolio.sh
cd portifolio.sh
```

### 2. Edite suas informações

Abra o `index.html` e substitua:

| Trecho | Onde encontrar |
|---|---|
| `jjoaobraz` | username do GitHub (3 ocorrências) |
| `João Braz` | seu nome |
| `Coordenador de Desenvolvimento de Projetos` | seu cargo |
| `Grupo Abraz` | sua empresa |
| `Olinda, PE` | sua cidade |
| `5581996364031` | seu número com DDI+DDD (sem `+`) |
| `joaorpa2021@gmail.com` | seu e-mail |
| URL do LinkedIn | seu perfil |

### 3. Edite os cards de serviço

Cada card segue essa estrutura no `index.html`:

```html
<div class="svc-card featured">   <!-- remova "featured" para borda branca -->

  <!-- Mockup visual (opcional) -->
  <div class="mockup mockup-browser"> ... </div>

  <!-- Badge: amber | violet | red -->
  <span class="svc-badge amber">🔥 Alta demanda</span>

  <h3 class="svc-title">Nome do Serviço</h3>
  <p class="svc-desc">Descrição curta do serviço.</p>

  <ul class="svc-features">
    <li>... feature 1</li>
    <li>... feature 2</li>
  </ul>

  <!-- Botão: svc-btn-main (verde) ou svc-btn-outline (borda) -->
  <a href="https://wa.me/SEU_NUMERO?text=..." class="svc-btn svc-btn-main">
    quero esse serviço
  </a>
</div>
```

#### Mockups disponíveis

| Classe | Visual |
|---|---|
| `mockup-browser` | Janela de browser com skeleton de landing page |
| `mockup-dashboard` | Painel administrativo com cards de stats |
| `mockup-terminal` | Terminal com output de script Python |
| `mockup-wpp` | Chat do WhatsApp com mensagens |
| `mockup-db` | Tabela MySQL com linhas de dados |

Para usar sem mockup, basta remover o bloco `<div class="mockup ...">`.

### 4. Teste localmente

```bash
python3 -m http.server 3000
# acesse http://localhost:3000
```

> **Importante:** abrir o `index.html` direto pelo arquivo não funciona para a GitHub API (bloqueio de CORS). Use sempre um servidor HTTP.

### 5. Suba para o GitHub

```bash
git init
git add .
git commit -m "feat: meu portfolio"
gh repo create portifolio.sh --public --source=. --remote=origin --push
```

### 6. Ative o GitHub Pages

```bash
gh api repos/<seu-usuario>/portifolio.sh/pages \
  -X POST \
  --field source[branch]=main \
  --field source[path]=/

gh api repos/<seu-usuario>/portifolio.sh/pages \
  -X PUT \
  --field build_type=workflow
```

Ou manualmente: **Settings → Pages → Source → GitHub Actions**

O site estará em: `https://<seu-usuario>.github.io/portifolio.sh`

---

## ⏱ WakaTime (opcional)

Mostra quantas horas você codou na última semana.

**1.** Pegue sua API key em [wakatime.com/settings/api-key](https://wakatime.com/settings/api-key)

**2.** No repositório: **Settings → Secrets and variables → Actions → New repository secret**
- Nome: `WAKATIME_API_KEY`
- Valor: sua key

**3.** Execute o workflow manualmente na aba **Actions → Update WakaTime Stats → Run workflow**

A partir daí ele roda automaticamente a cada hora.

---

## 📁 Estrutura

```
portifolio.sh/
├── index.html                    ← toda a estrutura da página
├── style.css                     ← estilos (paleta zinc + emerald)
├── main.js                       ← smooth scroll
├── wakatime.json                 ← dados do WakaTime (gerado pelo Action)
└── .github/
    └── workflows/
        ├── deploy.yml            ← publica no GitHub Pages a cada push
        └── wakatime.yml          ← atualiza wakatime.json a cada hora
```

---

## 🎨 Personalização rápida

### Trocar cor de destaque

No `style.css`, altere as variáveis `--em500` e `--em400`:

```css
:root {
  --em500: #10b981;  /* botões principais */
  --em400: #34d399;  /* textos e ícones de destaque */
}
```

Sugestões de paleta:
| Cor | `--em500` | `--em400` |
|---|---|---|
| Azul | `#3b82f6` | `#60a5fa` |
| Roxo | `#8b5cf6` | `#a78bfa` |
| Rosa | `#ec4899` | `#f472b6` |
| Laranja | `#f97316` | `#fb923c` |

### Adicionar redes sociais no footer

No `index.html`, dentro de `.footer-links`, adicione:

```html
<a href="https://instagram.com/seu-usuario" target="_blank" title="Instagram">
  <svg viewBox="0 0 24 24" fill="currentColor" width="16" height="16">
    <path d="M12 2.163c3.204 0 3.584.012 4.85.07..."/>
  </svg>
</a>
```

---

## 📄 Licença

MIT — use, modifique e distribua à vontade.
