# Checkpoint 1: Header

**Ponto de partida:** `base.html` (só HTML, sem estilo).
**Ponto de chegada:** variáveis, reset e header estilizado.

Arquivos: `index1.html` + `style.css`.

---

## 1. O que mudou no HTML

Quase nada. O header do `base.html` já tem o que precisamos:

- `id="busca"` no `<input>` → vira o seletor `#busca`.
- As demais regras usam as próprias tags: `header`, `nav ul`, `nav a`, `input`.

A única troca obrigatória é o `<link rel="stylesheet" href="style.css">` no `<head>`.

> Ao abrir este checkpoint, o **resto da página também muda** (fundo preto, fonte nova, listas sem recuo). As regras de base são **globais**, ou seja, valem para todos os elementos. É um bom momento para mostrar a cascata funcionando.

---

## 2. O que entrou no `style.css`

### Variáveis (`:root`)

```css
:root {
  --preto: #171717;
  --borda: 3px solid;
}
```

| Conceito | O que faz |
|---|---|
| `:root` | Representa a raiz do documento (`<html>`). O que é declarado nele vale para a página inteira. |
| `--nome: valor;` | **Variável CSS**: guarda um valor para reutilizar. Sempre começa com `--`. |
| `var(--nome)` | **Lê** a variável. `color: var(--preto)` é o mesmo que `color: #171717`. |
| `#171717` | Cor em hexadecimal (`#RRGGBB`). |
| `--borda: 3px solid;` | Guarda **parte** de um valor. Depois completamos com a cor: `border: var(--borda) var(--preto);` |

Para que serve: se a MAIN mudar o tom do magenta, alteramos uma linha e o site inteiro acompanha.

### Reset e base

| Regra | O que faz |
|---|---|
| `*` | **Seletor universal**: pega todos os elementos. |
| `box-sizing: border-box` | Faz `width`/`height` **incluírem** padding e borda (a conta fica mais fácil). |
| `margin: 0; padding: 0` | Zera os espaçamentos que o navegador coloca sozinho. |
| `background-color` / `color` | Fundo preto e texto branco na página toda. |
| `font-family: var(--fonte)` | Fonte Space Grotesk. Os filhos herdam do `body`. |
| `line-height: 1.5` | Altura da linha = 1,5 × o tamanho da fonte. Deixa o texto mais legível. |

### Header com Flexbox

```css
header {
  background-color: var(--magenta);
  padding: 16px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}
```

| Propriedade | O que faz |
|---|---|
| `padding: 16px 24px` | 2 valores: 16px em cima e embaixo, 24px nas laterais. |
| `display: flex` | Os filhos diretos (`h1`, `nav`, `input`) ficam lado a lado. |
| `justify-content: space-between` | Eixo horizontal: primeiro item na esquerda, último na direita, sobra dividida no meio. |
| `align-items: center` | Eixo vertical: centraliza os itens. |
| `gap: 16px` | Espaço mínimo **entre** os itens. Só funciona em flex ou grid. |

### Menu (`nav`)

| Regra | O que faz |
|---|---|
| `nav ul` / `nav a` | **Seletor descendente** (espaço): "o `ul` que está dentro do `nav`". |
| `display: flex; gap: 32px` | Links lado a lado com 32px entre eles. |
| `list-style: none` | Tira as bolinhas da lista. |
| `display: block` (no `a`) | O `<a>` é inline; como bloco, o padding e a borda funcionam por completo. |
| `text-decoration: none` | Tira o sublinhado do link. |
| `font-weight: 700` | Negrito (400 = normal, 700 = negrito). |
| `padding: 8px 14px` | Espaço interno do "botão". |
| `border: var(--borda) var(--preto)` | Vira `border: 3px solid #171717`. |

### Busca: especificidade na prática

```css
input { ... }            /* regra de TAG */
input:focus { ... }      /* TAG + pseudo-classe */
#busca { ... }           /* regra de ID */
#busca:focus { ... }     /* ID + pseudo-classe: vence o input:focus */
```

| Regra | O que faz |
|---|---|
| `font-family: inherit` | Campos de formulário **não herdam** a fonte sozinhos. `inherit` = "use a mesma do pai". |
| `font-size: 1rem` | `rem` = múltiplo da fonte da raiz (16px). `1rem` = 16px. |
| `:focus` | **Pseudo-classe**: o campo está selecionado (clicado ou via Tab). |
| `outline` / `outline-offset` | Contorno **fora** da borda (não ocupa espaço) e a distância dele até a borda. |
| `border-color` | Muda só a cor da borda. |
| `width: 260px` | Largura fixa da busca. |
| `outline-color` | Muda só a cor do contorno. |

**Demonstração:** o `input:focus` deixa o contorno turquesa, mas o `#busca:focus` deixa branco. Como **ID vence tag**, a busca fica com contorno branco.

---

## 3. Resumo dos conceitos deste checkpoint

- Variáveis CSS (`:root`, `--x`, `var()`)
- Seletor universal `*` e seletor descendente (`nav a`)
- Reset (`margin`, `padding`, `box-sizing`)
- Flexbox: `display: flex`, `justify-content`, `align-items`, `gap`
- Pseudo-classe `:focus`, `outline`
- Unidade `rem` e valor `inherit`
- Especificidade: `#busca` vencendo `input`
