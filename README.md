# Lash Pro 360° — Guia Completo de Configuração e Personalização

Este ficheiro explica como alterar cada parte da landing page sem precisar de conhecimentos de programação.

---

## 📁 Estrutura do ficheiro

O projeto é entregue num único ficheiro HTML (`lash-pro-360.html`) que podes abrir no browser ou publicar directamente.

---

## ⚙️ 1. Como alterar as configurações principais

Abre o ficheiro HTML num editor de texto (Notepad++, VS Code, ou até o Bloco de Notas).

Procura o bloco `const CONFIG = {` perto do início do ficheiro (dentro da tag `<script>`).

```js
const CONFIG = {
  PRODUCT_NAME: "Lash Pro 360°",
  PRODUCT_PRICE: "499 MT",
  OLD_PRICE: "2.600 MT",
  MPESA_NUMBER: "859025329",          // ← Altera aqui o número M-Pesa
  EMOLA_NUMBER: "870153542",          // ← Altera aqui o número e-Mola
  WHATSAPP_NUMBER: "258859025329",    // ← Com código do país, sem +
  PAYMENT_NAME: "Yurin Armindo",      // ← Nome para aparecer nas instruções
  CONTACT_EMAIL: "[EMAIL]",           // ← O teu e-mail de contacto
  ACCESS_LINK: "[ACCESS_LINK]",       // ← Link de acesso ao produto (ex: Google Drive)
  SPECIALIST_NAME: "[NOME]",
  META_PIXEL_ID: "[META_PIXEL_ID]",   // ← ID do teu Meta Pixel
  GOOGLE_ANALYTICS_ID: "[GA_ID]"      // ← ID Google Analytics
};
```

Guarda o ficheiro e abre no browser para ver as alterações.

---

## 💳 2. Como alterar o preço

No bloco `CONFIG`, altera:
```js
PRODUCT_PRICE: "499 MT",   // Preço actual
OLD_PRICE: "2.600 MT",      // Preço riscado
```

Depois, procura no HTML as instâncias de `499 MT` e `2.600 MT` para actualizar manualmente nos textos visíveis das secções.

---

## 📱 3. Como alterar os números M-Pesa e e-Mola

Apenas altera no bloco `CONFIG`:
```js
MPESA_NUMBER: "859025329",
EMOLA_NUMBER: "870153542",
PAYMENT_NAME: "Yurin Armindo",
```

Os valores aparecem automaticamente nas instruções de pagamento do checkout.

---

## 💬 4. Como alterar o WhatsApp

Altera no bloco `CONFIG`:
```js
WHATSAPP_NUMBER: "258859025329",
```

Usa o formato internacional sem o `+` — ex: `258849000000`

---

## 🖼️ 5. Como trocar as imagens

Procura os blocos com comentários `[Imagem da Especialista]`, `[Imagem do Manual]`, etc.

Para cada um, substitui o bloco de placeholder pela tag `<img>`:
```html
<!-- Antes: -->
<div class="hero-image-placeholder">...</div>

<!-- Depois: -->
<img src="caminho/para/a/tua/imagem.jpg" alt="Lash Designer" style="width:100%;height:100%;object-fit:cover">
```

**Formatos recomendados:**
- Hero: 800×1000px, WebP ou JPG
- Especialista: 600×800px
- Mockups: 800×600px

---

## 💬 6. Como adicionar depoimentos reais

Procura os 6 cards de depoimentos (começam com `<div class="testimonial-card">`).

Em cada um, substitui:
```html
[DEPOIMENTO REAL 01 — ...]
```
pelo texto real da aluna.

E substitui:
```html
[Nome da Aluna 01]
[Cidade, Moçambique]
[Foto]
```
pelos dados reais. Para a foto, usa:
```html
<img src="foto-aluna.jpg" alt="Nome" style="width:100%;height:100%;object-fit:cover;border-radius:50%">
```

---

## 👩‍💼 7. Como preencher os dados da especialista

Procura a secção `section-authority` e substitui os placeholders:
- `[NOME DA ESPECIALISTA]` → nome real
- `[Título / Especialidade]` → ex: "Lash Designer Certificada"
- `[BIO DA ESPECIALISTA]` → bio real
- `[N]` nos stats → números reais (anos de experiência, alunas, clientes)
- `[Foto]` → imagem real

---

## 🔐 8. Painel Administrativo

Acede ao painel admin clicando em "Admin" no rodapé da página.

**Senha padrão:** `lashpro2026`

Para alterar a senha, procura no ficheiro:
```js
const ADMIN_PASSWORD = 'lashpro2026';
```
E substitui pela senha que quiseres.

**O painel permite:**
- Ver todos os pagamentos enviados
- Filtrar por estado (pendente, aprovado, rejeitado)
- Pesquisar por nome ou número
- Aprovar ou rejeitar pagamentos
- Enviar o link de acesso directamente pelo WhatsApp

**Nota:** Os dados ficam guardados no localStorage do browser. Para uma solução de produção, integra com Supabase (ver secção abaixo).

---

## 🚀 9. Como publicar a landing page

### Opção A — Netlify (gratuito e rápido)
1. Vai a [netlify.com](https://netlify.com) e cria uma conta gratuita
2. Arrasta o ficheiro `lash-pro-360.html` para a área de deploy
3. A página fica online em segundos com URL automático
4. Para domínio próprio: em "Site settings" → "Domain management" → adiciona o teu domínio

### Opção B — Vercel
1. Vai a [vercel.com](https://vercel.com)
2. Cria uma pasta com o ficheiro renomeado para `index.html`
3. Faz o deploy pela interface web

### Opção C — Servidor próprio (cPanel/Hostinger/etc.)
1. Renomeia o ficheiro para `index.html`
2. Faz upload via File Manager ou FTP para a pasta `public_html`
3. Acede pelo teu domínio

---

## 🌐 10. Como configurar o domínio

Após publicares:
1. No teu registador de domínios (Namecheap, GoDaddy, etc.), vai às configurações DNS
2. Adiciona um registo `A` ou `CNAME` apontando para o servidor (o Netlify/Vercel fornece as instruções exactas)
3. Aguarda propagação (pode demorar até 48h, normalmente menos)

---

## 📊 11. Como activar o Meta Pixel

Procura `META_PIXEL_ID` no CONFIG e coloca o teu ID.

Depois, adiciona antes do `</head>` do ficheiro o código base do Meta Pixel (obtido no Facebook Business Manager):

```html
<script>
!function(f,b,e,v,n,t,s){...}
fbq('init', 'SEU_ID_AQUI');
fbq('track', 'PageView');
</script>
```

Os eventos `InitiateCheckout` e `SubmitPaymentProof` já estão configurados no código.

---

## 📈 12. Como activar o Google Analytics

Adiciona antes do `</head>`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

---

## 🗄️ 13. Integração com Supabase (backend completo)

Para ter os comprovativos guardados na nuvem em vez do localStorage:

### Tabela `payments` (SQL):
```sql
create table payments (
  id bigserial primary key,
  name text not null,
  whatsapp text not null,
  email text,
  payment_method text not null,
  payment_phone text not null,
  amount integer default 499,
  proof_url text,
  status text default 'pending',
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

### Storage bucket:
- Cria um bucket chamado `comprovativos` no Supabase Storage
- Define como privado

### Integração:
1. Instala `@supabase/supabase-js` (ou usa o CDN)
2. Substitui a função `submitProof` para fazer upload do ficheiro para o bucket e inserir o registo na tabela

---

## 📋 14. Checklist de lançamento

Antes de publicar:

- [ ] Alterar números M-Pesa e e-Mola no CONFIG
- [ ] Alterar nome de pagamento (PAYMENT_NAME)
- [ ] Alterar número WhatsApp
- [ ] Adicionar link de acesso ao produto (ACCESS_LINK)
- [ ] Adicionar dados reais da especialista
- [ ] Adicionar depoimentos reais (quando disponíveis)
- [ ] Trocar imagens placeholder por imagens reais
- [ ] Alterar senha do painel admin
- [ ] Testar fluxo completo de checkout
- [ ] Activar Meta Pixel (quando tiveres o ID)
- [ ] Testar em telemóvel (Samsung, iPhone)
- [ ] Publicar e configurar domínio

---

## 📞 Suporte

Para dúvidas técnicas, consulta este README ou contacta o desenvolvedor.

---

*Lash Pro 360° · Maputo, Moçambique · 2026*
