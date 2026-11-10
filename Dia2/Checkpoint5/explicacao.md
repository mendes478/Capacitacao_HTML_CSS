# Checkpoint 5: Seção 4 (resenhas)

**Ponto de partida:** Checkpoint 4.
**Ponto de chegada:** seção 4 com fundo magenta e as resenhas viradas cards que abrem e fecham, com `+` / `−` feito só com CSS.

---

## 1. O que mudou no HTML

| Antes (base) | Depois | Por quê |
|---|---|---|
| `<section>` | `<section id="resenhas" class="secao secao-magenta">` | Mesmo padrão das outras seções. |
| conteúdo solto | `<div class="conteudo">` + `<p class="subtitulo">` | Idem. |
| `<details>` | `<details class="resenha">` | Cada resenha vira um card. |
| `<p>`s soltos no `details` | `<div class="resenha-corpo"> ... </div>` | Agrupa a parte que aparece ao abrir, para dar padding só nela. |
| `<p><strong>Nota...</strong> <span>data</span></p>` | `<p class="resenha-data-avaliacao">` | Separa nota (esquerda) e data (direita). |

---

## 2. O que entrou no `style.css`

### Cor da seção

```css
.secao-magenta {
  background-color: var(--magenta);
  color: var(--branco);
}
```

### Card da resenha

| Regra | O que faz |
|---|---|
| `border` + `box-shadow` pretos | Moldura e sombra dura. |
| `margin-bottom: 24px` | Espaço entre um card e outro. |

### Título clicável (`summary`)

| Regra | O que faz |
|---|---|
| `display: flex; justify-content: space-between; align-items: center` | Título na esquerda e `+` na direita, centralizados na vertical. |
| `padding: 18px 20px` | Espaço interno. |
| `cursor: pointer` | Mãozinha: indica que dá para clicar. |
| `list-style: none` | Remove a setinha ▸ padrão do `<summary>`. |

### Pseudo-elemento `::after`

```css
.resenha summary::after {
  content: "+";
  font-size: 1.8rem;
  line-height: 1;
}
```

| Conceito | O que faz |
|---|---|
| `::after` | Cria um elemento "falso" como **último filho** do `summary`. Ele não existe no HTML, só no CSS. (O `::before` cria como primeiro filho.) |
| `content: "+"` | O texto do pseudo-elemento. **Obrigatório**: sem `content`, o `::after` não aparece. |
| `line-height: 1` | Evita que o `+` grande aumente a altura do título. |

Como o `summary` é flex, o `::after` vira mais um item flex e o `space-between` joga ele para a direita.

### Seletor de atributo `[open]`

```css
.resenha[open] summary { background-color: var(--turquesa); border-bottom: ...; }
.resenha[open] summary::after { content: "−"; }
```

| Conceito | O que faz |
|---|---|
| `[open]` | Seleciona o elemento que **tem** o atributo `open`. O navegador coloca `open` no `<details>` sozinho quando o usuário clica, e tira quando fecha. |
| troca do `content` | Aberto mostra `−`, fechado mostra `+`. Tudo sem JavaScript. |

### Corpo e linha de nota

| Regra | O que faz |
|---|---|
| `.resenha-corpo { padding: 20px }` | Espaço interno do texto. |
| `.resenha-data-avaliacao { margin-top: 1.4rem }` | Afasta a linha de nota do texto da resenha. |
| `display: flex; justify-content: space-between` | Nota na esquerda, data na direita. |
| `font-size: 0.9rem` | Texto um pouco menor. |

---

## 3. Resumo dos conceitos deste checkpoint

- Pseudo-elemento `::after` e a propriedade `content`
- Seletor de atributo `[open]`
- Estados aberto/fechado sem JavaScript
- Flex para separar itens nas pontas (`space-between`)
