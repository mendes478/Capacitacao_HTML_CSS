# Checkpoint 4: Seção 3 (formulário)

**Ponto de partida:** Checkpoint 3.
**Ponto de chegada:** seção 3 com fundo turquesa e o formulário num cartão preto, com os campos em coluna e botão com efeito.

---

## 1. O que mudou no HTML

| Antes (base) | Depois | Por quê |
|---|---|---|
| `<section>` (sem id) | `<section id="nova-midia" class="secao secao-turquesa">` | O `id` faz o link "Membros" do menu funcionar; as classes dão o estilo. |
| conteúdo solto | `<div class="conteudo">` + `<p class="subtitulo">` | Mesmo padrão das outras seções. |
| `<label>` + campo + `<br><br>` | `<div class="campo"> <label> + campo </div>` | Cada par label/campo vira um bloco. |
| `<button>` | `<button class="botao">` | Estilo próprio do botão. |
| campo "Data de lançamento" | removido | O site final não tem esse campo. |

> **Ponto importante:** sumiram todos os `<br>`. Antes o espaço era feito no HTML; agora quem cuida disso é o CSS (`gap`). **HTML = estrutura, CSS = aparência.**

---

## 2. O que entrou no `style.css`

### Cor da seção

`.secao-turquesa` segue a mesma ideia da `.secao-branco`: fundo turquesa, texto preto e as variáveis `--contorno` e `--sombra` que o formulário usa.

### Formulário com Flexbox em coluna

```css
form {
  max-width: 640px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
```

| Regra | O que faz |
|---|---|
| `max-width` + `margin: 0 auto` | Formulário mais estreito e centralizado. |
| `flex-direction: column` | Muda o eixo principal para **vertical**: os itens ficam um embaixo do outro. O padrão é `row` (lado a lado). |
| `gap: 20px` | Espaço entre os campos, no lugar dos `<br>`. |
| `.campo` (também flex em coluna) | Flex dentro de flex: label em cima, campo embaixo, 6px entre eles. |
| `label { font-weight: 700 }` | Labels em negrito. |

> Com `flex-direction: column`, os eixos **trocam**: `justify-content` passa a alinhar na vertical e `align-items` na horizontal.

### Campos

```css
form input, form select, form textarea { ... }
```

A regra `input` do header deixava os campos pretos. Aqui usamos um seletor descendente (`form input` = "input dentro do form"), que é **mais específico** que `input` sozinho, para deixar os campos do formulário brancos.

| Regra | O que faz |
|---|---|
| `form select:focus, form textarea:focus` | Contorno turquesa ao selecionar (o `input:focus` do header já cuida dos inputs). |
| `textarea { resize: vertical }` | O usuário só consegue redimensionar a caixa na altura. |

### Botão (`.botao`)

| Regra | O que faz |
|---|---|
| `cursor: pointer` | Mostra a "mãozinha", indicando que é clicável. |
| `box-shadow: 4px 4px 0 var(--magenta)` | Sombra dura magenta. |
| `transition: transform 0.15s, box-shadow 0.15s` | Quando essas propriedades mudarem, a mudança é **animada** em 0,15s em vez de "pular". |
| `.botao:hover` | Fundo branco, sobe 2px e a sombra cresce. |
| `.botao:focus` | Contorno magenta ao selecionar pelo teclado (acessibilidade). |

Compare com o card da seção 1: lá o `:hover` também usa `transform`, mas sem `transition`, então o card "pula" na hora. Aqui o botão se move suavemente.

---

## 3. Resumo dos conceitos deste checkpoint

- Espaçamento é papel do CSS, não do `<br>`
- `flex-direction: column` e flex dentro de flex
- Seletor descendente para vencer uma regra de tag (`form input`)
- `resize`, `cursor`
- `transition` para animar o `:hover`
