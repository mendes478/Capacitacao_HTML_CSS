# Checkpoint 3: Seção 2 (tabela)

**Ponto de partida:** Checkpoint 2.
**Ponto de chegada:** seção 2 com fundo branco e tabela escura, com cabeçalho turquesa, linhas zebradas e moldura com sombra.

---

## 1. O que mudou no HTML

| Antes (base) | Depois | Por quê |
|---|---|---|
| `<section id="atividade">` | `<section id="atividade" class="secao secao-branco">` | **Duas classes** separadas por espaço: `.secao` (estilo comum) + `.secao-branco` (só a cor). |
| conteúdo solto | `<div class="conteudo">` + `<p class="subtitulo">` | Reaproveita as classes do checkpoint anterior. |
| `<table>` solta | `<div class="moldura-tabela"><table>...</table></div>` | A `div` é a moldura (borda + sombra) e é ela que rola para o lado no celular. |
| `<td>★★★★★</td>` | `<td class="estrelas">★★★★★</td>` | Para pintar só as notas. |

> A seção já "nasce" com espaçamento e largura certos só por receber `.secao` e `.conteudo`. Essa é a vantagem das classes reutilizáveis.

---

## 2. O que entrou no `style.css`

### Cor da seção + variáveis locais

```css
.secao-branco {
  background-color: var(--branco);
  color: var(--preto);
  --contorno: var(--preto);
  --sombra: var(--magenta);
}
```

`.secao-branco` vem **depois** de `.secao` no arquivo e tem a mesma especificidade, então o fundo branco vence o preto.

As variáveis `--contorno` e `--sombra` são criadas **dentro** da classe, então só existem nos elementos dessa seção. A moldura da tabela usa `var(--contorno)` e `var(--sombra)`.

### Tabela

| Regra | O que faz |
|---|---|
| `overflow-x: auto` | Se a tabela for mais larga que a moldura, aparece uma barra de rolagem horizontal em vez de estourar a tela. |
| `box-shadow: 8px 8px 0 cor` | Sombra: deslocamento X, deslocamento Y, desfoque e cor. Desfoque `0` = sombra "dura", sem borrão. |
| `table { width: 100% }` | A tabela ocupa toda a moldura. |
| `border-collapse: collapse` | Junta as bordas vizinhas das células em uma só. |
| `th, td` | **Agrupamento** (vírgula): a mesma regra para os dois. |
| `text-align: left` | Texto à esquerda (o `<th>` vem centralizado por padrão). |
| `thead th` | Só as células do cabeçalho: fundo turquesa. |
| `tbody tr:nth-child(even)` | **Pseudo-classe** que seleciona pela posição: `even` = linhas pares. Cria o efeito **zebrado**. |
| `#2B2B2B` / `#3D3D3D` | Cinzas escuros, um pouco mais claros que o preto. |
| `tbody tr:hover` | A linha clareia com o mouse em cima. |
| `white-space: nowrap` | Não deixa quebrar a linha: as 5 estrelas ficam sempre juntas. |

**Para discutir em aula:** `tr:hover` vem **depois** de `nth-child(even)` e as duas têm a mesma especificidade. Em empate, **vence a última** no arquivo, por isso o hover funciona também nas linhas pares.

---

## 3. Resumo dos conceitos deste checkpoint

- Várias classes no mesmo elemento
- Variáveis criadas dentro de uma classe
- `overflow-x`, `box-shadow`, `border-collapse`
- Agrupamento de seletores (`th, td`)
- Pseudo-classe `:nth-child(even)`
- `white-space: nowrap`
- Cascata: em empate, vale a última regra
