# React Key

## Why a unique key?

3 momentos que um compoente é renderizado novamente no React

1. Quando o estado altera;
2. Quando a propriedade (props) altera.
3. Quando um componente pai renderiza novamente

---

## Isso pode cause lentidão?

1, 2, 3, 4

1, 2, 3, 4, 5

Se precisar renderizar novamente uma lista, ele compara todas as key para saber oque estava em tela e renderizar somente as novas keys

## Why don't use the array's index?

Caso um item mude de posição, se estivessemos usando o index como key, o React entende que o valor mudo, mas o index não e renderiza tudo novamente, mesmo os valores não mundado

```js
// index keeps the same even though the value change

const post = [1, 2, 3, 4, 5];
// index -> 0, 1, 2, 3, 4
const post = [1, 2, 5, 3, 4];
// index -> 0, 1, 2, 3, 4
// index keeps the same

// The id change with the value

const postWithId = [1, 2, 3, 4, 5];
// id -> 0, 1, 2, 3, 4
const post = [1, 2, 5, 3, 4];
// id -> 0, 1, 4, 2, 3
```
