# PASTA DO MARCENEIRO — Briefing Completo para Desenvolvimento

> Stack: HTML + CSS + JS vanilla (sem framework)
> Deploy: GitHub + Vercel
> Público: marceneiro autônomo, acessa pelo celular
> Prioridade: mobile-first, carregamento rápido, sem dependências pesadas

---

# PARTE 1 — DESIGN SYSTEM

## Paleta de cores

A identidade visual remete a madeira nobre, profissionalismo de ofício e seriedade de quem trabalha com as mãos. Foge do azul técnico da concorrência (marmorista) e do verde genérico de "dinheiro".

```
--cor-fundo:        #0F0D0B   /* quase preto com tom amadeirado */
--cor-fundo-alt:    #1A1612   /* seções alternadas, levemente mais claro */
--cor-superficie:   #221E19   /* cards e caixas */
--cor-borda:        #2E2820   /* bordas sutis */

--cor-primaria:     #C8833A   /* âmbar queimado — tom de madeira envernizada */
--cor-primaria-soft:#C8833A22 /* versão transparente para backgrounds */
--cor-acento:       #E8C070   /* dourado claro — highlight e textos em destaque */

--cor-positivo:     #4A9B6F   /* verde musgo — ícones de check */
--cor-negativo:     #9B4A4A   /* vermelho apagado — ícones de X */

--cor-texto:        #F0EBE3   /* branco quente, não puro */
--cor-texto-suave:  #A09080   /* textos secundários */
--cor-texto-muted:  #6B5E50   /* microcopy, rodapé */
```

## Tipografia

Duas fontes do Google Fonts — carregadas com `display=swap`:

```
--fonte-display: 'Sora', sans-serif;
/* Usada em: headlines, números grandes, nome do produto */
/* Pesos: 700 (headlines) e 800 (hero headline) */

--fonte-corpo: 'Inter', sans-serif;
/* Usada em: parágrafos, bullets, botões, microcopy */
/* Pesos: 400 (corpo), 500 (bullets), 600 (botões, labels) */
```

Import no `<head>`:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@700;800&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```

## Escala tipográfica

```
--text-xs:    11px   /* microcopy, badges */
--text-sm:    13px   /* bullets, corpo secundário */
--text-base:  15px   /* corpo principal */
--text-lg:    18px   /* subheadlines, destaque */
--text-xl:    22px   /* headlines de seção mobile */
--text-2xl:   28px   /* headlines de seção desktop */
--text-3xl:   36px   /* hero headline mobile */
--text-4xl:   48px   /* hero headline desktop */
--text-price: 64px   /* preço em destaque */
```

## Espaçamentos

```
--gap-xs:   8px
--gap-sm:   16px
--gap-md:   24px
--gap-lg:   48px
--gap-xl:   80px
--gap-2xl:  120px

/* Padding lateral das seções */
--px-mobile:  20px
--px-desktop: 0  /* centralizado com max-width */

/* Max-width do conteúdo */
--max-content: 960px
--max-narrow:  640px   /* seções de texto puro */
```

## Border-radius

```
--radius-sm:  8px    /* badges, inputs */
--radius-md:  12px   /* cards pequenos */
--radius-lg:  20px   /* cards principais */
--radius-full: 9999px /* botões e badges pill */
```

## Sombras

```
--shadow-card: 0 2px 20px rgba(0,0,0,0.4);
--shadow-cta:  0 8px 32px rgba(200, 131, 58, 0.35);
--shadow-cta-hover: 0 12px 40px rgba(200, 131, 58, 0.5);
```

---

# PARTE 2 — COMPONENTES GLOBAIS

## Botão CTA principal

```css
.btn-cta {
  background: linear-gradient(135deg, #C8833A, #E8C070);
  color: #0F0D0B;
  font-family: var(--fonte-corpo);
  font-weight: 600;
  font-size: 16px;
  padding: 16px 32px;
  border-radius: var(--radius-full);
  border: none;
  cursor: pointer;
  box-shadow: var(--shadow-cta);
  transition: all 0.2s ease;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  text-decoration: none;
  white-space: nowrap;
}

.btn-cta:hover {
  box-shadow: var(--shadow-cta-hover);
  transform: translateY(-1px);
}

.btn-cta:active {
  transform: translateY(0);
}
```

## Sobretítulo (eyebrow label)

```css
.eyebrow {
  font-family: var(--fonte-corpo);
  font-size: var(--text-xs);
  font-weight: 600;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--cor-primaria);
}
```

## Card padrão

```css
.card {
  background: var(--cor-superficie);
  border: 1px solid var(--cor-borda);
  border-radius: var(--radius-lg);
  padding: 24px;
  transition: border-color 0.2s ease;
}

.card:hover {
  border-color: var(--cor-primaria-soft);
}
```

## Ícone check / X

```css
.icon-check { color: var(--cor-positivo); width: 18px; height: 18px; flex-shrink: 0; }
.icon-x     { color: var(--cor-negativo); width: 18px; height: 18px; flex-shrink: 0; }
```

Use SVG inline — sem dependência de biblioteca de ícones.

Check SVG:
```html
<svg class="icon-check" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="3 10 8 15 17 5"/></svg>
```

X SVG:
```html
<svg class="icon-x" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="4" y1="4" x2="16" y2="16"/><line x1="16" y1="4" x2="4" y2="16"/></svg>
```

## Seção wrapper padrão

```css
.section {
  padding: var(--gap-xl) var(--px-mobile);
}

.section-alt {
  background: var(--cor-fundo-alt);
}

.section-inner {
  max-width: var(--max-content);
  margin: 0 auto;
}

.section-narrow {
  max-width: var(--max-narrow);
  margin: 0 auto;
}
```

---

# PARTE 3 — ESTRUTURA E COMPORTAMENTO DAS SEÇÕES

## SEÇÃO 1 — HERO

**Layout:** duas colunas no desktop (texto esquerda, imagem direita), coluna única no mobile.

**Comportamento:**
- Hero ocupa 100vh no desktop, altura natural no mobile
- Imagem do lado direito: mockup do produto (tablet mostrando o catálogo) com leve rotação (transform: rotate(3deg)) e sombra profunda
- Fundo: gradiente radial sutil saindo do centro-alto `radial-gradient(ellipse at 30% 20%, #2A1E0F 0%, #0F0D0B 60%)`
- Badge animado: entra com `fade-in` de 0.3s ao carregar a página
- Headline: entra com `slide-up` de 0.5s, delay 0.1s
- Subheadline e bullets: `slide-up`, delay 0.2s
- Botão: `slide-up`, delay 0.3s
- Seta animada no botão: `translateX` pulsando suavemente em loop (2s)

**Microcopy abaixo do botão:** ícones inline + texto numa linha só, separados por bullet `•`

**Copy:**

Badge: `Pasta do Marceneiro`

Headline:
```
O cliente não some porque seu preço é alto.
Ele some porque não enxergou o valor antes de ver o número.
```

Subheadline:
```
Um kit pronto pra você apresentar seus projetos com profissionalismo,
fechar mais e parar de baixar preço pra não perder a venda.
```

Bullets:
- Catálogo pronto pra mandar no WhatsApp
- Modelos de cozinha, quarto, closet, home office e área de serviço
- Checklist que evita erro de medida e retrabalho
- Planilha pra orçar sem chute
- Mensagens prontas pra conduzir o cliente até o fechamento

Caixa de reforço (borda âmbar, fundo levemente diferente):
```
Não é curso. Não é aula.
É uma pasta digital pronta pra usar hoje, no celular, na frente do cliente.
```

CTA: `Quero minha Pasta do Marceneiro →`

Microcopy: `Acesso imediato • Abre no celular • Garantia de 7 dias • Pagamento único`

---

## SEÇÃO 2 — O PROBLEMA REAL

**Layout:** coluna única, centralizado, max-width 640px

**Fundo:** `var(--cor-fundo-alt)`

**Comportamento:**
- Animação scroll-trigger: headline e corpo entram com `fade-in + slide-up` quando a seção entra na viewport (IntersectionObserver)
- Frase de impacto: caixa separada, borda esquerda de 3px na cor âmbar, padding generoso, fonte maior

**Copy:**

Eyebrow: `O problema real`

Headline:
```
Baixar preço não faz o cliente confiar mais em você.
Só ensina ele a pedir mais desconto.
```

Corpo:
```
Quando você manda uma foto e um valor, o cliente não tem como saber
por que o seu trabalho vale mais que o do concorrente.

Então ele faz a única coisa que consegue: compara pelo preço.
```

Frase de impacto (bloco destacado):
```
"Cliente só pechincha quando não enxerga diferença."
```

---

## SEÇÃO 3 — ANTES E DEPOIS

**Layout:** dois cards lado a lado no desktop, empilhados no mobile

**Comportamento:**
- Os dois cards entram com animação simultânea ao scroll
- Card esquerdo (improviso): borda vermelha apagada `rgba(155,74,74,0.3)`
- Card direito (Pasta): borda âmbar `rgba(200,131,58,0.3)`, fundo levemente diferente
- Cada item da lista: ícone X ou Check antes do texto

**Copy:**

Eyebrow: `A diferença na prática`

Headline: `O mesmo projeto, apresentado de dois jeitos diferentes.`

Coluna A — `No improviso` (título em vermelho apagado):
- Manda foto do catálogo do fornecedor
- Passa o preço sem contexto
- Procura referência perdida na galeria
- Cliente acha caro e some
- Você baixa o preço pra tentar salvar

Coluna B — `Com a Pasta do Marceneiro` (título em verde musgo):
- Mostra catálogo organizado por ambiente
- Explica acabamentos e materiais com segurança
- Apresenta uma proposta profissional
- Cliente entende o valor antes do preço
- Você fecha sem precisar dar desconto

---

## SEÇÃO 4 — O MÉTODO

**Layout:** 4 cards em linha no desktop, 2x2 no tablet, 1 coluna no mobile

**Fundo:** `var(--cor-fundo-alt)`

**Comportamento:**
- Cards entram em sequência com stagger de 0.1s cada (scroll-trigger)
- Número grande (01, 02...) no topo do card: fonte Sora 700, cor âmbar, tamanho 40px
- Hover no card: borda muda de `--cor-borda` para `var(--cor-primaria-soft)`
- Linha conectora entre os cards no desktop: linha horizontal pontilhada na cor `--cor-borda`

**Copy:**

Eyebrow: `Como funciona`

Headline: `Um jeito simples de apresentar antes de falar preço.`

Cards:

`01 — Mostre`
Abra o catálogo e deixe o cliente visualizar o ambiente dele antes de qualquer valor.

`02 — Explique`
Mostre a diferença entre acabamentos e materiais. O cliente precisa entender por que uma opção custa mais.

`03 — Confira`
Use o checklist na visita pra não esquecer medida, tomada, encanamento ou detalhe que vira retrabalho.

`04 — Feche`
Envie a proposta profissional e use os scripts pra conduzir até o sim, sem baixar preço.

Frase de fechamento (caixa destacada, centralizada):
```
"Quando o cliente entende o projeto,
o preço deixa de ser o assunto principal."
```

---

## SEÇÃO 5 — O QUE VEM DENTRO

**Layout:** grid 3 colunas desktop, 2 colunas tablet, 1 coluna mobile

**Comportamento:**
- Cada card tem: número do item (eyebrow), título, descrição, e área de mockup no rodapé do card
- Área de mockup: placeholder com borda tracejada e label `[imagem: mockup item X]` — substituir por imagem real após produção
- Cards entram com stagger ao scroll
- CTA repetido abaixo do grid

**Copy:**

Eyebrow: `Conteúdo`

Headline: `Tudo que vem na Pasta do Marceneiro`

Item 01 — Catálogo de Ambientes
Modelos de cozinha, quarto, closet, home office, sala e área de serviço, separados por estilo, prontos pra mostrar no WhatsApp.

Item 02 — Guia de Acabamentos
A diferença visual entre MDF, laca, texturizado e madeira natural. Pra você justificar o preço sem enrolar.

Item 03 — Checklist de Visita Técnica
Tudo que precisa conferir no imóvel antes de fechar: medida, tomada, encanamento, parede fora de esquadro e mais.

Item 04 — Planilha de Orçamento
Coloca material, mão de obra e margem, e o preço final sai sem chute.

Item 05 — Guia de Materiais e Ferragens
Pra você falar com segurança sobre chapa, ferragem, corrediça e acabamento na frente do cliente.

Item 06 — Scripts de WhatsApp
Mensagens prontas pra cada etapa: primeiro contato, follow-up, cliente que pede desconto e cliente que sumiu.

Item 07 — Modelo de Proposta Profissional
Um orçamento formatado que passa muito mais confiança que um preço solto no WhatsApp.

CTA abaixo do grid: `Quero minha Pasta do Marceneiro →`

---

## SEÇÃO 6 — BÔNUS

**Layout:** grid 3 colunas desktop, 1 coluna mobile

**Fundo:** `var(--cor-fundo-alt)`

**Comportamento:**
- Badge `BÔNUS` em cada card: pill âmbar com texto escuro
- Cards com borda âmbar translúcida
- Animação stagger ao scroll

**Copy:**

Eyebrow: `Bônus`

Headline: `Você ainda recebe três bônus junto`

Bônus 1 — Catálogo Premium de Alto Valor
Closets, cozinhas gourmet e home offices sofisticados, pra você subir o ticket e vender projetos maiores.

Bônus 2 — Guia de Quanto Cobrar por M²
Referências de preço por tipo de móvel e acabamento, pra você ter segurança na hora de passar o valor.

Bônus 3 — Mensagens pra Cliente que Pede Desconto
Respostas prontas pra defender seu preço sem parecer desesperado.

---

## SEÇÃO 7 — PROVA SOCIAL

**Layout:** grid 2 colunas desktop, 1 coluna mobile

**Comportamento:**
- Seção marcada com `id="depoimentos"` e atributo `data-visible="false"` por padrão
- Exibir apenas quando depoimentos reais forem adicionados
- Estilo dos cards: fundo superfície, borda sutil, foto redonda do depoente no topo, nome + cidade abaixo, texto do depoimento
- Se usar print de WhatsApp: imagem dentro do card com border-radius

**Copy:**

Eyebrow: `Quem já usa`

Headline: `Marceneiros que pararam de vender no improviso`

> PLACEHOLDER: inserir 3 a 4 depoimentos reais aqui.
> Formato preferido: foto do rosto + nome + cidade + texto curto (2-3 linhas)
> Alternativa: print de conversa de WhatsApp com resultado

---

## SEÇÃO 8 — QUEBRA DE OBJEÇÕES

**Layout:** lista de pares (crença → verdade), 1 coluna, max-width 720px, centralizado

**Comportamento:**
- Cada par: dois blocos lado a lado no desktop, empilhados no mobile
- Bloco esquerdo (crença): label `CRENÇA` em vermelho apagado, texto em `--cor-texto-suave`
- Bloco direito (verdade): label `A VERDADE` em verde musgo, texto em `--cor-texto` com font-weight 500
- Divisão entre os blocos: linha vertical no desktop, linha horizontal no mobile
- Animação: pares entram com stagger ao scroll

**Copy:**

Eyebrow: `Antes de decidir`

Headline: `Talvez você esteja perdendo projeto por um motivo que nem percebeu.`

Par 1:
CRENÇA: "Cliente de marcenaria só quer preço."
A VERDADE: Ele quer o mais barato quando tudo parece igual. Dê o que comparar e o preço deixa de ser o único critério.

Par 2:
CRENÇA: "Foto no WhatsApp já resolve."
A VERDADE: Foto solta mostra um móvel. Catálogo organizado mostra uma solução.

Par 3:
CRENÇA: "Projeto bonito é coisa de arquiteto."
A VERDADE: Você não precisa ser arquiteto pra apresentar seu trabalho com organização.

Par 4:
CRENÇA: "Eu faço orçamento de cabeça."
A VERDADE: Orçamento na pressa esconde custo, margem e prejuízo.

Par 5:
CRENÇA: "R$17 não deve entregar muita coisa."
A VERDADE: R$17 é menos que o prejuízo de um projeto perdido por falta de apresentação.

---

## SEÇÃO 9 — OFERTA

**Layout:** card central, max-width 560px, centralizado

**Fundo da seção:** `var(--cor-fundo-alt)`

**Comportamento:**
- Card com borda âmbar brilhante, sombra `var(--shadow-cta)` difusa ao redor
- Preço riscado: `text-decoration: line-through`, cor `--cor-texto-muted`
- Preço final: fonte Sora 800, tamanho `var(--text-price)`, cor `--cor-acento`
- CTA dentro do card: largura total no mobile
- Selos abaixo do CTA em linha: ícone cadeado + "Compra segura", ícone raio + "Acesso imediato", ícone escudo + "7 dias de garantia"

**Copy:**

Eyebrow: `Oferta`

Headline: `Receba hoje a Pasta do Marceneiro`

Lista "Você recebe":
- Catálogo de Ambientes
- Guia de Acabamentos
- Checklist de Visita Técnica
- Planilha de Orçamento
- Guia de Materiais e Ferragens
- Scripts de WhatsApp
- Modelo de Proposta Profissional

Label bônus: `BÔNUS INCLUSOS`
- Catálogo Premium de Alto Valor
- Guia de Quanto Cobrar por M²
- Mensagens pra Cliente que Pede Desconto

Preço:
```
De R$97
Por apenas
R$17
Pagamento único • Material digital pra usar no celular
```

Justificativa:
```
Menos que uma chapa de MDF.
Menos que um projeto perdido por falta de apresentação.
```

CTA: `Receber agora por R$17 →`

---

## SEÇÃO 10 — GARANTIA

**Layout:** card centralizado, max-width 480px, ícone de escudo grande no topo

**Comportamento:**
- Ícone de escudo: 80x80px, cor âmbar, animação suave de `scale` ao entrar na viewport
- Borda do card: verde musgo translúcido `rgba(74,155,111,0.3)`

**Copy:**

Headline: `Garantia simples de 7 dias`

Corpo:
```
Receba o material, abra no celular e veja se faz sentido pra sua rotina.

Se sentir que não te ajuda a apresentar, orçar ou fechar melhor,
pede o reembolso dentro de 7 dias. Sem burocracia.
```

---

## SEÇÃO 11 — PRA QUEM É / NÃO É

**Layout:** dois cards lado a lado desktop, empilhados mobile

**Fundo:** `var(--cor-fundo-alt)`

**Comportamento:**
- Card esquerdo (é pra você): borda verde musgo translúcida
- Card direito (não é pra você): borda vermelha apagada translúcida
- Título de cada card: verde ou vermelho conforme o tom

**Copy:**

Headline: `Essa pasta é pra você?`

É pra você se:
- Trabalha com móveis planejados ou marcenaria
- Atende cliente pelo WhatsApp
- Quer parar de mandar foto solta
- Cansou de baixar preço pra não perder venda
- Quer apresentar seu trabalho com mais profissionalismo

Não é pra você se:
- Procura promessa de dinheiro fácil
- Quer um curso longo com aulas teóricas
- Não pretende usar material digital no atendimento
- Quer continuar vendendo no improviso

---

## SEÇÃO 12 — FAQ

**Layout:** lista de acordeões, coluna única, max-width 640px, centralizado

**Comportamento:**
- Acordeão nativo com `<details>` + `<summary>` estilizados
- Ícone `+` que rotaciona 45° quando aberto (CSS transition)
- Borda do item ativa muda para âmbar translúcido
- Apenas um item aberto por vez (JS simples)
- Animação de abertura: `max-height` transition de 0 ao conteúdo

**Copy:**

Eyebrow: `Dúvidas`

Headline: `Perguntas frequentes`

Como recebo o material?
Depois da confirmação do pagamento, você recebe tudo por e-mail pra abrir no celular.

Preciso de computador?
Não. Foi feito pra abrir no celular. Também funciona em tablet e computador.

É curso?
Não. É uma pasta digital pronta pra consultar, apresentar e orçar no dia a dia.

Serve pra quem trabalha sozinho?
Sim. Foi feito pra autônomos e pequenas marcenarias que atendem pelo WhatsApp.

Posso usar com meus clientes?
Sim. O catálogo e os modelos são pra você apresentar direto pro cliente.

Tem garantia?
Sim, 7 dias. Se não servir pra sua rotina, pede reembolso.

É material físico?
Não. É digital, em PDF.

---

## SEÇÃO 13 — FECHAMENTO

**Layout:** coluna única, centralizado, max-width 600px

**Fundo:** gradiente de `var(--cor-fundo-alt)` para `var(--cor-fundo)`

**Comportamento:**
- Headline grande, centralizado
- CTA largura total no mobile
- Essa é a última ancora antes do rodapé — tom de escolha binária, sem enrolação

**Copy:**

Headline:
```
Você vai continuar baixando preço
ou vai começar a mostrar valor antes do número?
```

Corpo:
```
Dá pra continuar mandando foto e esperando o cliente decidir só pelo preço.

Ou dá pra abrir a Pasta do Marceneiro, apresentar seu trabalho com
organização e fechar sem abrir mão da sua margem.
```

CTA: `Quero minha Pasta do Marceneiro →`

Microcopy: `Acesso imediato • Pagamento único de R$17 • Garantia de 7 dias`

---

## BOTÃO FLUTUANTE (mobile only)

**Comportamento:**
- Aparece após o usuário passar do hero (scroll > 100vh)
- Desaparece quando o usuário chega na seção de oferta (para não sobrepor)
- Posição: fixed, bottom: 16px, left: 50%, transform: translateX(-50%)
- Entra com `slide-up` de 0.3s, sai com `slide-down`
- Sombra forte para destacar sobre o conteúdo

**Texto:** `Receber por R$17 →`

---

# PARTE 4 — ANIMAÇÕES

## Definições CSS

```css
@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes slide-up {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes slide-down {
  from { opacity: 1; transform: translateY(0); }
  to   { opacity: 0; transform: translateY(20px); }
}

@keyframes pulse-x {
  0%, 100% { transform: translateX(0); }
  50%       { transform: translateX(4px); }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

## IntersectionObserver (scroll-trigger)

```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('is-visible');
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('[data-animate]').forEach(el => observer.observe(el));
```

Classe base para elementos animados:
```css
[data-animate] {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}

[data-animate].is-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Stagger via atributo data-delay */
[data-animate][data-delay="1"] { transition-delay: 0.1s; }
[data-animate][data-delay="2"] { transition-delay: 0.2s; }
[data-animate][data-delay="3"] { transition-delay: 0.3s; }
[data-animate][data-delay="4"] { transition-delay: 0.4s; }
```

---

# PARTE 5 — HEAD E META

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pasta do Marceneiro — Feche mais projetos sem baixar preço</title>
<meta name="description" content="Kit digital com catálogo, checklist, planilha e scripts prontos pra marceneiro apresentar melhor, orçar com segurança e fechar sem dar desconto. Acesso imediato por R$17.">
<meta property="og:title" content="Pasta do Marceneiro">
<meta property="og:description" content="Feche mais projetos sem baixar preço. Kit digital por R$17.">
<meta property="og:type" content="website">
```

---

# PARTE 6 — LINK DO CHECKOUT

Substitua `LINK_DO_CHECKOUT` em todos os botões CTA pelo link real da plataforma de pagamento (Wiapy, Hotmart, Kiwify ou similar).

```html
<a href="LINK_DO_CHECKOUT" class="btn-cta">Quero minha Pasta do Marceneiro →</a>
```

---

# PARTE 7 — ORDEM DAS SEÇÕES

1. Hero
2. Problema Real
3. Antes e Depois
4. O Método
5. O Que Vem Dentro
6. Bônus
7. Prova Social *(oculta até ter depoimentos reais)*
8. Quebra de Objeções
9. Oferta
10. Garantia
11. Pra Quem É / Não É
12. FAQ
13. Fechamento
14. Rodapé simples (nome do produto + "Material digital • Pagamento único • Garantia de 7 dias")

