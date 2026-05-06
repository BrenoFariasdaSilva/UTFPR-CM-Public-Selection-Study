# Árvores de Pesquisa  
*(Search Trees)*

---

# 3.1 Conceitos básicos (Basic Concepts)

## Definição de árvore
Uma **árvore** é uma estrutura de dados hierárquica composta por nós:
- Nó raiz
- Nós filhos
- Sem ciclos
- Caminho único entre nós

---

## Terminologia
- Raiz (root)
- Folha (leaf)
- Nó interno
- Altura (height)
- Profundidade (depth)

---

# 3.2 Árvores binárias

## Estrutura em C
```c
typedef struct No {
    int valor;
    struct No* esq;
    struct No* dir;
} No;
```

---

# 3.3 Árvores Binárias de Busca (BST)

## Inserção
```c
No* inserir(No* raiz, int x) {
    if (raiz == NULL) {
        No* novo = malloc(sizeof(No));
        novo->valor = x;
        novo->esq = novo->dir = NULL;
        return novo;
    }
    if (x < raiz->valor)
        raiz->esq = inserir(raiz->esq, x);
    else
        raiz->dir = inserir(raiz->dir, x);
    return raiz;
}
```

## Busca
```c
No* buscar(No* raiz, int x) {
    if (raiz == NULL || raiz->valor == x)
        return raiz;
    if (x < raiz->valor)
        return buscar(raiz->esq, x);
    return buscar(raiz->dir, x);
}
```

## Remoção
```c
No* minValor(No* no) {
    while (no->esq != NULL)
        no = no->esq;
    return no;
}

No* remover(No* raiz, int x) {
    if (raiz == NULL) return raiz;

    if (x < raiz->valor)
        raiz->esq = remover(raiz->esq, x);
    else if (x > raiz->valor)
        raiz->dir = remover(raiz->dir, x);
    else {
        if (raiz->esq == NULL) {
            No* temp = raiz->dir;
            free(raiz);
            return temp;
        }
        else if (raiz->dir == NULL) {
            No* temp = raiz->esq;
            free(raiz);
            return temp;
        }

        No* temp = minValor(raiz->dir);
        raiz->valor = temp->valor;
        raiz->dir = remover(raiz->dir, temp->valor);
    }
    return raiz;
}
```

---

# Percursos

## In-order
```c
void inorder(No* raiz) {
    if (raiz != NULL) {
        inorder(raiz->esq);
        printf("%d ", raiz->valor);
        inorder(raiz->dir);
    }
}
```

## Pre-order
```c
void preorder(No* raiz) {
    if (raiz != NULL) {
        printf("%d ", raiz->valor);
        preorder(raiz->esq);
        preorder(raiz->dir);
    }
}
```

## Post-order
```c
void postorder(No* raiz) {
    if (raiz != NULL) {
        postorder(raiz->esq);
        postorder(raiz->dir);
        printf("%d ", raiz->valor);
    }
}
```

---

# 3.4 Complexidade
- O(h)
- Melhor: O(log n)
- Pior: O(n)

---

# 3.5 Árvores balanceadas

## AVL
- Fator de balanceamento: -1, 0, 1

## Red-Black
- Altura O(log n)
- Regras de cores

---

# COMO CAI NA PROVA
- Definir árvore e BST
- Explicar remoção
- Implementar em C
- Analisar complexidade

---

# CONCLUSÃO
- Estruturas eficientes
- Base para algoritmos avançados
