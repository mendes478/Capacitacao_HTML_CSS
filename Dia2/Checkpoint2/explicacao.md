# Checkpoint 2: Seção 1 (vitrine em Grid)

**Ponto de partida:** Checkpoint 1.
**Ponto de chegada:** seção 1 com conteúdo centralizado, ranking com números coloridos e os pôsteres numa grade de cards.

---

## 1. O que mudou no HTML

| Antes (base) | Depois | Por quê |
|---|---|---|
| `<section id="recomendadas">` | `<section id="recomendadas" class="secao">` | Estilo comum a todas as seções. |
| conteúdo solto | `<div class="conteudo"> ... </div>` | Caixa que limita a largura e centraliza. |
| `<p>` | `<p class="subtitulo">` | Espaço embaixo do texto de introdução. |
| `<ol>` | `<ol class="ranking">` | Para estilizar só essa lista. |
| imagens e textos soltos | `<div class="vitrine">` com vários `<article class="card">` | A vitrine é o **grid**; cada card é **uma célula**. Sem o `article`, a imagem, o título e o texto virariam células separadas. |
| `<img ...>` | `<a href="../../Filme.html"><img ...></a>` | Clicar no pôster leva à página do filme. |
| `<span class="badge">` | `<span class="midia-classificacao">` | Nome mais claro: a etiqueta diz se é filme, série, livro ou jogo. |

A seção passa a ter 8 cards, iguais aos do site final.

---

## 2. O que entrou no `style.css`

### Seção e conteúdo

```css
.secao { background-color: var(--preto); border-top: 4px solid var(--preto); padding: 72px 24px; }
.conteudo { max-width: 1100px; margin: 0 auto; }
.subtitulo { margin-bottom: 32px; }
```

| Regra | O que faz |
|---|---|
| `.secao` | Classe **reutilizável**: as outras seções também vão usar. |
| `border-top` | Borda só em cima, separando as seções. |
| `padding: 72px 24px` | 72px em cima e embaixo, 24px nas laterais. |
| `max-width: 1100px` | O conteúdo cresce até 1100px e para. Em telas menores, encolhe. |
| `margin: 0 auto` | `auto` nas laterais divide o espaço que sobra igualmente → **centraliza**. |
| `margin-bottom` | Margem só embaixo. |

Por que uma `div` separada: a `section` pinta o fundo de ponta a ponta da tela, e a `div.conteudo` mantém o texto numa coluna de 1100px no meio.

### Ranking

| Regra | O que faz |
|---|---|
| `margin: 8px 0 40px 24px` | 4 valores, sentido horário: cima, direita, baixo, esquerda. Os 24px da esquerda devolvem o recuo que o reset tirou (senão os números somem). |
| `.ranking li::marker` | **Pseudo-elemento**: o número de cada item. Pintamos de magenta e negrito. |

### Grid

```css
.vitrine {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 28px;
}
```

| Propriedade | O que faz |
|---|---|
| `display: grid` | Os filhos diretos (`article`) viram células da grade. |
| `grid-template-columns` | Define as colunas. |
| `repeat(4, 1fr)` | Atalho para `1fr 1fr 1fr 1fr`: 4 colunas iguais. |
| `fr` | Fração do espaço livre: cada coluna fica com 1/4. |
| `gap: 28px` | Espaço entre linhas e colunas. |

Com 8 cards e 4 colunas, o grid cria as 2 linhas sozinho.

### Card

| Regra | O que faz |
|---|---|
| `padding: 12px` | Espaço branco entre a borda e o pôster. |
| `border: var(--borda) var(--turquesa)` | Borda turquesa de 3px. |
| `.card:hover` | **Pseudo-classe** `:hover`: vale enquanto o mouse está em cima. |
| `transform: translate(-4px, -4px)` | Move o card 4px para a esquerda e 4px para cima, sem empurrar os vizinhos. |
| `.card img { width: 100% }` | A imagem acompanha a largura do card. Sem isso, ela fica com os 300px originais e estoura o grid. |

### Etiqueta (`.midia-classificacao`)

| Regra | O que faz |
|---|---|
| `display: inline-block` | Fica na linha como inline, mas aceita padding e margin verticais como bloco. |
| `font-size: 0.8rem` | 80% do tamanho base (≈ 12,8px). |
| `padding: 2px 10px` | 2px em cima e embaixo, 10px nas laterais. |
| `border: 2px solid var(--preto)` | Borda fina preta. |
| `margin: 12px 0 6px` | 3 valores: cima, laterais, baixo. |

---

## 3. Resumo dos conceitos deste checkpoint

- Classes reutilizáveis (`.secao`, `.conteudo`, `.subtitulo`)
- Centralização com `max-width` + `margin: 0 auto`
- Atalhos de `margin`/`padding` com 2, 3 e 4 valores
- Pseudo-elemento `::marker`
- CSS Grid: `grid-template-columns`, `repeat()`, `fr`, `gap`
- Pseudo-classe `:hover` + `transform: translate()`
- `display: inline-block`
