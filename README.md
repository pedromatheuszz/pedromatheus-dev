# Landing Page — Pedro Matheus da Silva Machado

Landing page pessoal de desenvolvedor web / engenheiro de software.
HTML, CSS e JavaScript puros — **sem build, sem dependências, sem node_modules**.

---

## Rodando localmente

Abrir o `index.html` direto no navegador funciona, mas o ideal é servir por HTTP
(o botão "copiar e-mail" usa a Clipboard API, que exige contexto seguro):

```bash
python -m http.server 4321
```

Depois acesse `http://localhost:4321`.

---

## Estrutura

| Arquivo      | Conteúdo                                                         |
|--------------|------------------------------------------------------------------|
| `index.html` | Toda a marcação, dividida por seções comentadas                   |
| `styles.css` | Design tokens, componentes, seções e breakpoints                  |
| `script.js`  | Tema, menu, scrollspy, reveal, copiar e-mail, validação do form   |

---

## ⚠️ O que você PRECISA editar antes de publicar

### 1. Projetos (obrigatório — conteúdo de exemplo)

A seção `<section id="projetos">` contém **três cards de exemplo**. Eles estão
marcados com um comentário `PLACEHOLDER` no HTML. Para cada `<article class="work">`:

- troque `.work__type`, `.work__title` e `.work__desc`;
- ajuste os `<li>` dentro de `.chips`;
- aponte o `href` de `.work__link` para o repositório ou site do projeto real
  (hoje todos apontam para `#contato`).

Para adicionar mais projetos, duplique o bloco `<article class="work">` inteiro.
O grid se ajusta sozinho. As capas usam três variantes de cor: `work__cover--a`
(âmbar), `--b` (ciano) e `--c` (terracota).

### 2. URL canônica

No `<head>`, troque `<link rel="canonical" href="https://exemplo.com/">` pelo
seu domínio real.

### 3. Conferir os textos

Bio, serviços e processo foram escritos com base nas informações fornecidas.
Revise o tom e ajuste o que não corresponder à sua realidade — principalmente a
seção **Serviços**, que descreve o que você se propõe a entregar.

---

## WhatsApp

Número configurado: **(47) 99648-2391** → `+55 47 99648-2391` → `wa.me/5547996482391`.

Aparece em três lugares, **todos com a mesma URL**:

1. Botão principal na seção de contato (`.wa`)
2. Linha "WhatsApp" da ficha técnica, na seção Sobre
3. Botão flutuante, que surge após o hero e some quando o botão principal
   entra na tela

### Mensagem pré-preenchida

O parâmetro `?text=` é o que o **visitante envia para você** — não é uma
mensagem sua para ele. Por isso está escrita na voz do cliente:

> Olá, Pedro! Vi seu portfólio e gostei do seu trabalho. Tenho um projeto em
> mente e gostaria de conversar sobre ele.

Ela é curta de propósito: mensagens longas o visitante apaga antes de enviar.

Para mudar o texto, gere a URL codificada (não escreva os acentos direto no
`href`):

```bash
node -e "console.log(encodeURIComponent('Sua nova mensagem aqui'))"
```

Cole o resultado depois de `?text=` **nas três ocorrências** em `index.html`.
Elas precisam continuar idênticas.

### Trocar o número

Substitua `5547996482391` nos três links e o `telephone` no bloco JSON-LD.
O formato é país + DDD + número, só dígitos, sem `+` nem espaços.

> Publicar o número expõe ele a coleta automatizada e spam. É o padrão para
> quem vende serviço, mas vale saber.

---

## Formulário de contato

O envio abre o cliente de e-mail do visitante (`mailto:`) com assunto e corpo
já preenchidos. **Não há back-end** — nada é armazenado nem enviado a terceiros.

Se quiser recebimento direto na caixa de entrada sem depender do cliente de
e-mail do visitante, troque a lógica em `initForm()` (`script.js`) por um POST
para um serviço como Formspree, Web3Forms ou Resend.

O destinatário está em `script.js`:

```js
var DESTINATARIO = 'pedromatheusdasilva123@gmail.com';
```

---

## Identidade visual

### Arquivos gerados a partir do logotipo

| Arquivo | Tamanho | Onde é usado |
|---------|---------|--------------|
| `logo-mark.png` | 512×512 | Monograma no topo e no rodapé |
| `logo.png` | 969×624 | Logotipo completo, para reuso |
| `og-image.png` | 1200×630 | Prévia ao compartilhar o link |
| `apple-touch-icon.png` | 180×180 | Ícone ao salvar na tela inicial |
| `favicon.png` | 64×64 | Ícone da aba |

Todos foram recortados do arquivo original. Para regerá-los depois de alterar o
logotipo, os recortes usados foram: monograma em `x 354, y 309, 542×507` e
logotipo completo em `x 183, y 343, 909×564`.

O monograma mantém o fundo escuro do logotipo **nos dois temas**. Isso é
intencional: o "P" é branco e sumiria sobre o papel claro. No tema claro ele
funciona como um selo.

### Paleta

As cores vieram dos pixels do próprio logotipo:

| Origem | Valor |
|--------|-------|
| Fundo do logotipo | `#040404` |
| Branco do logotipo | `#eff0f2` |
| Azul da marca | `#5460f0` |
| Gradiente do "M" | `#4878f0` → `#6054fc` |

Os tokens ficam no topo do `styles.css`:

```css
[data-theme="dark"]  { --a1: #5460f0; --a1-text: #7b86f6; }
[data-theme="light"] { --a1: #3a44cc; --a1-text: #3a44cc; }
```

**Por que dois tokens de azul.** O azul da marca rende apenas 4.08:1 sobre o
fundo escuro, abaixo do mínimo de 4.5:1 da WCAG AA. `--a1` é usado em
preenchimentos (botões, ícones, o ponto das etapas), onde a exigência é menor;
`--a1-text` é uma variação clareada da mesma cor, com 6.24:1, usada em todo
texto. Se trocar um, ajuste o outro e remeça o contraste.

A paleta tem três eixos: `--a1` (azul da marca), `--a2` (ciano) e `--a3`
(âmbar, contraponto quente). Mantenha os três distintos para o visual não
achatar em uma cor só.

O tema inicial segue a preferência do sistema operacional e é persistido em
`localStorage` sob a chave `pm-theme`. A meta tag `theme-color` lê `--bg` do
CSS em tempo de execução, então não precisa ser atualizada à mão.

---

## Publicando

Por ser um site estático, qualquer uma destas opções serve — todas gratuitas:

- **GitHub Pages** — suba os arquivos num repositório e ative Pages em Settings;
- **Netlify / Vercel** — arraste a pasta na interface, ou conecte o repositório;
- **Cloudflare Pages** — conecte o repositório, sem build command.

Nenhuma exige etapa de build.

---

## Acessibilidade e SEO já implementados

- Estrutura semântica com landmarks (`header`, `main`, `section`, `footer`)
- Skip link para o conteúdo principal
- Estados de foco visíveis em todos os elementos interativos
- `aria-expanded`, `aria-pressed`, `aria-invalid` e `role="alert"` nos erros
- `prefers-reduced-motion` desativa animações e o scroll suave
- Progressive enhancement: as animações de entrada só escondem o conteúdo se a
  classe `.js` existir no `<html>`. Se o `script.js` não carregar ou o JS estiver
  desativado, a página aparece inteira. Há ainda um timeout de 2s que revela tudo
  caso o `IntersectionObserver` não dispare (aba aberta em segundo plano)
- Meta description, Open Graph, Twitter Card e JSON-LD (`schema.org/Person`)
- `lang="pt-BR"` e estilo de impressão dedicado

---

## Navegadores

Chrome, Edge, Firefox e Safari em versões recentes. Usa `color-mix()`,
`IntersectionObserver` e `backdrop-filter`; em navegadores antigos a página
continua legível, apenas sem os refinamentos visuais.
