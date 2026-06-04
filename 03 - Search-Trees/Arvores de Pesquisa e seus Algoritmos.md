# Árvores de pesquisa e seus algoritmos

## 1. Introdução

Árvores de pesquisa ocupam posição central na organização eficiente de dados ordenáveis. Elas suportam busca, inserção e remoção de forma hierárquica e, quando balanceadas, aproximam-se do limite informacional ótimo para operações de dicionário. A relevância acadêmica dessas estruturas decorre do fato de que elas conectam fundamentos combinatórios, provas de corretude, análise probabilística e engenharia de armazenamento secundário (Cormen et al., 2009; Knuth, 1998).

Além das árvores binárias e árvores binárias de busca, o ecossistema inclui variantes auto-balanceadas como AVL e Red-Black Trees, bem como árvores multiway como B-Trees, fundamentais em sistemas de arquivos e bancos de dados. Cada família materializa um compromisso diferente entre rigidez de balanceamento, custo de atualização, localidade em memória e adequação a hierarquias de armazenamento.

## 2. Fundamentação Teórica

### 2.1 Conceitos básicos

Uma árvore é um grafo conexo e acíclico. Em árvores enraizadas, cada nó possui um pai, exceto a raiz, e zero ou mais filhos. A altura influencia diretamente o custo de operações de pesquisa. Em árvores de busca, a relação de ordem entre chaves permite decidir localmente o próximo ramo a seguir, reduzindo o espaço de busca a cada passo.

### 2.2 Balanceamento

Se a altura de uma árvore binária de busca degenera para $n - 1$, as operações tornam-se lineares. O objetivo de estruturas balanceadas é restringir a altura para $\Theta(\log n)$. AVL faz isso com critério rígido de diferença de alturas. Red-Black Trees empregam coloração e regras menos estritas para reduzir número de rotações. B-Trees redistribuem chaves em páginas com múltiplos filhos, otimizando acesso em disco (Sedgewick, 1998; Cormen et al., 2012).

## 3. Desenvolvimento

```mermaid
flowchart TD
    A[Busca de chave k] --> B{No atual nulo?}
    B -->|Sim| C[Fracasso]
    B -->|Nao| D{chave = no.chave?}
    D -->|Sim| E[Sucesso]
    D -->|Nao e chave menor| F[Subarvore esquerda]
    D -->|Nao e chave maior| G[Subarvore direita]
```

### 3.1 Árvores binárias e percursos

Árvores binárias são estruturas hierárquicas nas quais cada nó possui, no máximo, dois filhos, convencionalmente denominados filho esquerdo e filho direito. Essa organização permite representar relações hierárquicas de forma eficiente e serve como base para diversas estruturas mais avançadas, como árvores AVL, Red-Black Trees e heaps.

Os percursos fundamentais em árvores binárias são:

#### Percurso em pré-ordem

O percurso em pré-ordem visita primeiro a raiz da subárvore corrente e depois percorre recursivamente os filhos esquerdo e direito. É frequentemente utilizado para serialização de árvores, cópia de estruturas hierárquicas e representação de expressões prefixadas.

**Pseudocódigo**

```text
algoritmo pre_ordem(no)
    se no = nulo então retorne

    visite(no)
    pre_ordem(no.esq)
    pre_ordem(no.dir)
fim
```

#### Percurso em-ordem

O percurso em-ordem visita a subárvore esquerda antes da raiz e a subárvore direita depois da raiz. Em árvores binárias de busca (BST), esse percurso produz os elementos em ordem crescente, sendo amplamente utilizado para exibição ordenada de dados.

**Pseudocódigo**

```text
algoritmo em_ordem(no)
    se no = nulo então retorne

    em_ordem(no.esq)
    visite(no)
    em_ordem(no.dir)
fim
```

#### Percurso em pós-ordem

O percurso em pós-ordem processa completamente os descendentes antes de visitar a raiz. É amplamente utilizado em operações de remoção de árvores, liberação de memória e avaliação de expressões pós-fixadas.

**Pseudocódigo**

```text
algoritmo pos_ordem(no)
    se no = nulo então retorne

    pos_ordem(no.esq)
    pos_ordem(no.dir)
    visite(no)
fim
```

A implementação das operações básicas de busca, inserção e remoção geralmente utiliza recursão. Em árvores binárias de busca, a propriedade fundamental estabelece que todos os valores da subárvore esquerda são menores que a chave do nó atual e todos os valores da subárvore direita são maiores, permitindo buscas eficientes quando a árvore permanece balanceada.

| Estrutura              | Facilidade de implementação | Facilidade de uso | Desempenho              | Consumo de memória | Vantagens                      | Desvantagens                    | Casos de uso          | Big O típico              |
| ---------------------- | --------------------------- | ----------------- | ----------------------- | ------------------ | ------------------------------ | ------------------------------- | --------------------- | ------------------------- |
| Árvore binária simples | Média                       | Média             | Dependente da forma     | O(n)               | Modela hierarquia naturalmente | Sem garantia de busca eficiente | Expressões, parsing   | Busca O(n)                |
| BST                    | Média                       | Alta              | Muito bom se balanceada | O(n)               | Busca orientada por ordem      | Pode degenerar                  | Dicionários ordenados | Média O(log n), pior O(n) |

#### Algoritmo 1: BST com inserção

**Exemplo de construção de uma BST.** Considere a inserção das chaves:

```text
50, 30, 70, 20, 40, 60, 80
```

A árvore resultante é:

```text
                50
              /    \
            30      70
           /  \    /  \
         20   40  60   80
```

Por exemplo:

* Buscar a chave 60 percorre os nós 50 → 70 → 60.
* Inserir a chave 65 adicionaria um novo nó à direita de 60.
* Remover a chave 70 exigiria a substituição pelo seu sucessor em-ordem (80 ou 60, dependendo da estratégia adotada).

```

**Pseudocódigo**

```text
algoritmo bst_inserir(no, chave)
    se no = nulo então
        retorne novo_no(chave)
    fim

    se chave < no.chave então
        no.esq <- bst_inserir(no.esq, chave)

    senao se chave > no.chave então
        no.dir <- bst_inserir(no.dir, chave)
    fim

    retorne no

fim

algoritmo bst_remover(no, chave)
    se no = nulo então
        retorne nulo
    fim

    se chave < no.chave então
        no.esq <- bst_remover(no.esq, chave)

    senao se chave > no.chave então
        no.dir <- bst_remover(no.dir, chave)

    senao
        se no.esq = nulo então
            temp <- no.dir
            libere(no)
            retorne temp
        fim

        se no.dir = nulo então
            temp <- no.esq
            libere(no)
            retorne temp
        fim

        sucessor <- minimo(no.dir)
        no.chave <- sucessor.chave
        no.dir <- bst_remover(no.dir, sucessor.chave)
    fim

    retorne no
fim

algoritmo bst_buscar(no, chave)
    se no = nulo ou no.chave = chave então
        retorne no
    fim

    se chave < no.chave então
        retorne bst_buscar(no.esq, chave)
    fim

    retorne bst_buscar(no.dir, chave)
fim
```

**Implementação completa em C**

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct NoArvore {
    int chave;
    int altura;
    struct NoArvore *esquerda;
    struct NoArvore *direita;
} NoArvore;

NoArvore *bst_criar_no(int chave) {
    NoArvore *no = (NoArvore *)malloc(sizeof(NoArvore));
    if (no == NULL) {
        return NULL;
    }
    no->chave = chave;
    no->altura = 1;
    no->esquerda = NULL;
    no->direita = NULL;
    return no;
}

NoArvore *bst_buscar(NoArvore *raiz, int chave) {
    if (raiz == NULL || raiz->chave == chave) {
        return raiz;
    }
    if (chave < raiz->chave) {
        return bst_buscar(raiz->esquerda, chave);
    }
    return bst_buscar(raiz->direita, chave);
}

NoArvore *bst_inserir(NoArvore *raiz, int chave) {
    if (raiz == NULL) {
        return bst_criar_no(chave);
    }
    if (chave < raiz->chave) {
        raiz->esquerda = bst_inserir(raiz->esquerda, chave);
    } else if (chave > raiz->chave) {
        raiz->direita = bst_inserir(raiz->direita, chave);
    }
    return raiz;
}

NoArvore *bst_minimo(NoArvore *raiz) {
    while (raiz != NULL && raiz->esquerda != NULL) {
        raiz = raiz->esquerda;
    }
    return raiz;
}

NoArvore *bst_remover(NoArvore *raiz, int chave) {
    if (raiz == NULL) {
        return NULL;
    }

    if (chave < raiz->chave) {
        raiz->esquerda = bst_remover(raiz->esquerda, chave);
    } else if (chave > raiz->chave) {
        raiz->direita = bst_remover(raiz->direita, chave);
    } else {
        if (raiz->esquerda == NULL) {
            NoArvore *temp = raiz->direita;
            free(raiz);
            return temp;
        }
        if (raiz->direita == NULL) {
            NoArvore *temp = raiz->esquerda;
            free(raiz);
            return temp;
        }

        NoArvore *sucessor = bst_minimo(raiz->direita);
        raiz->chave = sucessor->chave;
        raiz->direita = bst_remover(raiz->direita, sucessor->chave);
    }

    return raiz;
}

void bst_inorder(const NoArvore *raiz) {
    if (raiz == NULL) {
        return;
    }
    bst_inorder(raiz->esquerda);
    printf("%d ", raiz->chave);
    bst_inorder(raiz->direita);
}
```

**Complexidade.** Busca, inserção e remoção custam $O(h)$, em que $h$ é a altura. Melhor e médio caso aproximam-se de $O(\log n)$; pior caso $O(n)$. Espaço recursivo também é $O(h)$.

**Explicação das partes relevantes.** A remoção com dois filhos substitui a chave pelo sucessor em-ordem; a busca preserva a propriedade de ordem local; a profundidade recursiva acompanha a altura da árvore.

### 3.2 AVL

Árvores AVL são árvores binárias de busca autobalanceadas nas quais o fator de balanceamento de cada nó deve permanecer em $\{-1, 0, 1\}$. O fator de balanceamento é definido como a diferença entre as alturas das subárvores esquerda e direita. Essa restrição mantém a altura da árvore em $O(\log n)$, garantindo operações eficientes de busca, inserção e remoção.

**Exemplo de árvore AVL.** O fator de balanceamento de cada nó é calculado como a diferença entre as alturas das subárvores esquerda e direita. Em uma árvore AVL válida, esse valor deve permanecer entre -1 e 1.

```text
                     30 (0)
                   /        \
               20 (0)      40 (0)
              /    \       /    \
          10 (0) 25 (0) 35 (0) 50 (0)
```

Legenda:

* Valor entre parênteses = fator de balanceamento.
* Todos os nós possuem fator de balanceamento igual a 0.
* A árvore encontra-se perfeitamente balanceada.
* A altura cresce proporcionalmente a $\log n$.

Por exemplo, o percurso em-ordem produz:

```text
10, 20, 25, 30, 35, 40, 50
```

Quando uma operação provoca desequilíbrio, rotações simples ou duplas são utilizadas para restaurar o balanceamento da estrutura.

#### Rotação simples à direita

A rotação simples à direita é aplicada quando ocorre um desequilíbrio do tipo esquerda-esquerda (LL), isto é, quando a inserção ocorre na subárvore esquerda do filho esquerdo.

**Pseudocódigo**

```text
algoritmo rotacao_direita(y)
    x <- y.esq
    t2 <- x.dir

    x.dir <- y
    y.esq <- t2

    atualize_alturas(x, y)

    retorne x
fim
```

#### Rotação simples à esquerda

A rotação simples à esquerda é aplicada quando ocorre um desequilíbrio do tipo direita-direita (RR), isto é, quando a inserção ocorre na subárvore direita do filho direito.

**Pseudocódigo**

```text
algoritmo rotacao_esquerda(x)
    y <- x.dir
    t2 <- y.esq

    y.esq <- x
    x.dir <- t2

    atualize_alturas(x, y)

    retorne y
fim
```

#### Rotação dupla esquerda-direita (LR)

A rotação dupla esquerda-direita é utilizada quando a inserção ocorre na subárvore direita do filho esquerdo. Nesse caso, executa-se inicialmente uma rotação à esquerda e depois uma rotação à direita.

**Pseudocódigo**

```text
algoritmo rotacao_esquerda_direita(no)
    no.esq <- rotacao_esquerda(no.esq)

    retorne rotacao_direita(no)
fim
```

#### Rotação dupla direita-esquerda (RL)

A rotação dupla direita-esquerda é utilizada quando a inserção ocorre na subárvore esquerda do filho direito. Nesse caso, executa-se inicialmente uma rotação à direita e depois uma rotação à esquerda.

**Pseudocódigo**

```text
algoritmo rotacao_direita_esquerda(no)
    no.dir <- rotacao_direita(no.dir)

    retorne rotacao_esquerda(no)
fim
```

#### Algoritmo 2: Inserção em árvore AVL

Após inserir um novo elemento seguindo as regras de uma BST, a árvore atualiza as alturas dos nós e verifica possíveis desequilíbrios. Caso o fator de balanceamento ultrapasse os limites permitidos, a rotação apropriada é aplicada.

**Pseudocódigo**

```text
algoritmo avl_inserir(raiz, chave)
    se raiz = nulo então
        retorne novo_no(chave)
    fim

    se chave < raiz.chave então
        raiz.esq <- avl_inserir(raiz.esq, chave)

    senao se chave > raiz.chave então
        raiz.dir <- avl_inserir(raiz.dir, chave)

    senao
        retorne raiz
    fim

    atualize_altura(raiz)

    fator <- fator_balanceamento(raiz)

    se fator > 1 e chave < raiz.esq.chave então
        retorne rotacao_direita(raiz)
    fim

    se fator < -1 e chave > raiz.dir.chave então
        retorne rotacao_esquerda(raiz)
    fim

    se fator > 1 e chave > raiz.esq.chave então
        retorne rotacao_esquerda_direita(raiz)
    fim

    se fator < -1 e chave < raiz.dir.chave então
        retorne rotacao_direita_esquerda(raiz)
    fim

    retorne raiz
fim
```

A principal vantagem das árvores AVL é a garantia de altura limitada por $O(\log n)$, evitando a degeneração observada em árvores binárias de busca convencionais. Como consequência, operações de busca, inserção e remoção mantêm desempenho logarítmico mesmo em cenários desfavoráveis.

#### Algoritmo 2: rotações e inserção AVL

**Implementação completa em C**

```c
int maximo(int a, int b) {
    return (a > b) ? a : b;
}

int avl_altura(NoArvore *no) {
    return (no == NULL) ? 0 : no->altura;
}

int avl_fator_balanceamento(NoArvore *no) {
    return (no == NULL) ? 0 : avl_altura(no->esquerda) - avl_altura(no->direita);
}

NoArvore *avl_rotacao_direita(NoArvore *y) {
    NoArvore *x = y->esquerda;
    NoArvore *t2 = x->direita;

    x->direita = y;
    y->esquerda = t2;

    y->altura = 1 + maximo(avl_altura(y->esquerda), avl_altura(y->direita));
    x->altura = 1 + maximo(avl_altura(x->esquerda), avl_altura(x->direita));
    return x;
}

NoArvore *avl_rotacao_esquerda(NoArvore *x) {
    NoArvore *y = x->direita;
    NoArvore *t2 = y->esquerda;

    y->esquerda = x;
    x->direita = t2;

    x->altura = 1 + maximo(avl_altura(x->esquerda), avl_altura(x->direita));
    y->altura = 1 + maximo(avl_altura(y->esquerda), avl_altura(y->direita));
    return y;
}

NoArvore *avl_inserir(NoArvore *raiz, int chave) {
    if (raiz == NULL) {
        return bst_criar_no(chave);
    }

    if (chave < raiz->chave) {
        raiz->esquerda = avl_inserir(raiz->esquerda, chave);
    } else if (chave > raiz->chave) {
        raiz->direita = avl_inserir(raiz->direita, chave);
    } else {
        return raiz;
    }

    raiz->altura = 1 + maximo(avl_altura(raiz->esquerda), avl_altura(raiz->direita));
    int fator = avl_fator_balanceamento(raiz);

    if (fator > 1 && chave < raiz->esquerda->chave) {
        return avl_rotacao_direita(raiz);
    }
    if (fator < -1 && chave > raiz->direita->chave) {
        return avl_rotacao_esquerda(raiz);
    }
    if (fator > 1 && chave > raiz->esquerda->chave) {
        raiz->esquerda = avl_rotacao_esquerda(raiz->esquerda);
        return avl_rotacao_direita(raiz);
    }
    if (fator < -1 && chave < raiz->direita->chave) {
        raiz->direita = avl_rotacao_direita(raiz->direita);
        return avl_rotacao_esquerda(raiz);
    }

    return raiz;
}
```

**Complexidade.** Busca, inserção e remoção em $O(\log n)$; espaço adicional $O(\log n)$ via recursão.

**Comparação com BST.** AVL reduz rigorosamente a altura e tende a favorecer consultas, mas paga esse ganho com manutenção de alturas e rotações adicionais.

### 3.3 Red-Black Trees

Árvores rubro-negras impõem invariantes de cor: a raiz é preta, nós vermelhos não possuem filhos vermelhos, e todo caminho da raiz a uma folha nula tem a mesma altura negra. O balanceamento é menos rígido que em AVL, o que geralmente reduz rotações em atualizações.

```text
Propriedades essenciais:
1. Cada nó é vermelho ou preto.
2. A raiz é preta.
3. Folhas nulas são pretas.
4. Nenhum nó vermelho tem filho vermelho.
5. Todos os caminhos possuem mesma altura negra.
```

**Pseudocódigo resumido da inserção.** Inserir como em BST, colorir o novo nó de vermelho e corrigir violações por recoloração e rotações, conforme a cor do tio. A remoção é mais complexa, envolvendo casos de nó vermelho ou preto e ajustes subsequentes para manter invariantes.

**Exemplo de violação após inserção.**

Após inserir a chave 10:

```text
        30(B)
        /
     20(R)
     /
  10(R)
```

A propriedade "nenhum nó vermelho possui filho vermelho" foi violada.

Após uma rotação à direita e ajuste de cores:

```text
         20(B)
        /     \
    10(R)    30(R)
```

A árvore volta a satisfazer as propriedades rubro-negras.

**Complexidade.** Busca, inserção e remoção em $O(\log n)$. Em bibliotecas de propósito geral, elas são frequentemente preferidas a AVL por melhor equilíbrio prático entre custo de manutenção e altura controlada. A vantagem de uma árvore rubro-negra é que ela é mais flexível em termos de balanceamento, o que pode resultar em menos rotações durante inserções e remoções, especialmente em cenários com muitas atualizações. No entanto, a implementação é mais complexa devido à necessidade de manter as invariantes de cor e realizar as rotações corretas.
