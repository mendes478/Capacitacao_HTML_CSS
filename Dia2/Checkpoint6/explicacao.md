# Checkpoint 6: Footer (site completo)

**Ponto de partida:** Checkpoint 5.
**Ponto de chegada:** rodapé estilizado. Com isso, todas as partes do site estão prontas.

---

## 1. O que mudou no HTML

| Antes (base) | Depois | Por quê |
|---|---|---|
| `<h3>` e `<p>` soltos no footer | `<div class="rodape-texto"> <h3> + <p> </div>` | O footer vira flex. Sem a `div`, o `h3` e o `p` seriam **dois itens** e ficariam lado a lado. Com a `div`, viram **um item só**. Ela nem precisa de CSS. |
| `<h3>MAINbox</h3>` | `<h3>MAINboxd</h3>` | Correção do nome. |
| `<p>` | `<p style="margin-top: 8px;">` | Exemplo de **CSS inline**: tem a maior prioridade na cascata. Bom para mostrar em aula, mas evite no dia a dia. |
| `<ul>` | `<ul class="redes-sociais">` | Lista de redes estilizada. |

---

## 2. O que entrou no `style.css`

### Footer

```css
footer {
  background-color: var(--preto);
  border-top: 4px solid var(--turquesa);
  padding: 32px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}
```

É a **mesma receita do header**: flex com o texto numa ponta e as redes na outra.

| Regra | O que faz |
|---|---|
| `border-top: 4px solid var(--turquesa)` | Faixa turquesa separando o rodapé da seção magenta. |
| `padding: 32px 24px` | 32px em cima e embaixo, 24px nas laterais. |
| `justify-content: space-between` | Texto na esquerda, redes na direita. |
| `align-items: center` | Centraliza na vertical. |
| `gap: 20px` | Espaço mínimo entre os dois blocos. |

### Redes sociais

| Regra | O que faz |
|---|---|
| `.redes-sociais { display: flex; list-style: none; gap: 20px }` | Links lado a lado, sem bolinhas. |
| `.redes-sociais a { color: var(--branco) }` | Sem essa regra, o link fica **azul** (cor padrão do navegador), quase invisível no fundo preto. |
| `font-weight: 700` | Negrito. |
| `.redes-sociais a:hover { color: var(--turquesa) }` | O link fica turquesa com o mouse em cima. |

---

## 3. Resumo dos conceitos deste checkpoint

- Reaproveitar a receita de flex do header
- `div` como agrupador de itens flex
- CSS inline (`style="..."`) e sua prioridade
- Cor padrão dos links e como trocar
