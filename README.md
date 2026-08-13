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

### 2. Links sociais (obrigatório)

Em `<ul class="socials">`, os dois links estão como `href="#"`:

```html
<a href="https://github.com/SEU-USUARIO" rel="noopener">
<a href="https://linkedin.com/in/SEU-PERFIL" rel="noopener">
```

Se não quiser algum deles, apague o `<li>` correspondente.
O WhatsApp já está configurado (veja abaixo).

### 3. URL canônica e imagem social

No `<head>`:

- `<link rel="canonical" href="https://exemplo.com/">` → seu domínio real;
- `<meta property="og:image" content="og-image.png">` → crie um `og-image.png`
  de **1200×630 px** na raiz do projeto. Sem ele, o link compartilhado no
  WhatsApp/LinkedIn aparece sem imagem.

### 4. Conferir os textos

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

## Personalizando o visual

Todas as cores, fontes e espaçamentos são variáveis CSS no topo do `styles.css`.

Trocar o acento principal (âmbar) em **ambos os temas**:

```css
[data-theme="dark"]  { --a1: #e8a33d; --a1-soft: rgba(232,163,61,.13); }
[data-theme="light"] { --a1: #a06209; --a1-soft: rgba(160,98,9,.10); }
```

A paleta tem três eixos de acento — `--a1` (âmbar), `--a2` (ciano) e `--a3`
(terracota) — usados nas tags de stack e nas capas de projeto. Mantenha os três
distintos para o visual não achatar em uma cor só.

O tema inicial segue a preferência do sistema operacional e é persistido em
`localStorage` sob a chave `pm-theme`.

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
