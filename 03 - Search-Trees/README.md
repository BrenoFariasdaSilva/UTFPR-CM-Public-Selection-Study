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
- **Raiz (root):** nó inicial da árvore, sem pai.
- **Folha (leaf):** nó sem filhos.
- **Nó interno:** nó que não é raiz nem folha, possui pelo menos um filho.
- **Altura (height):** maior distância da raiz até uma folha.
- **Profundidade (depth):** distância do nó até a raiz.

---

## Tipos de Árvores

- **Árvore completa:** todos os níveis, exceto possivelmente o último, estão totalmente preenchidos e todos os nós estão o mais à esquerda possível.
- **Árvore cheia (ou estritamente binária):** cada nó tem 0 ou 2 filhos (nunca apenas 1).
- **Árvore balanceada:** diferença de altura entre subárvores à esquerda e à direita de qualquer nó é no máximo 1.
- **Árvore desbalanceada:** diferença de altura entre subárvores é maior que 1, o que pode levar a operações ineficientes.
- **Árvore degenerada:** cada nó tem apenas um filho, tornando-se semelhante a uma lista ligada.
- **Árvore incompleta:** não preenche os critérios de completa ou cheia; pode ter níveis intermediários parcialmente preenchidos.

---

## Tipos quanto ao número de filhos

- **Árvore binária:** cada nó tem no máximo 2 filhos.
- **Árvore ternária:** cada nó tem no máximo 3 filhos.
- **Árvore m-ária:** cada nó tem no máximo m filhos (ex: árvore 4-ária, árvore 5-ária, etc).

Essas classificações determinam a estrutura e as aplicações possíveis para cada tipo de árvore.

---

# 3.2 Árvores binárias
Árvore binária é uma estrutura de dados onde cada nó tem no máximo dois filhos, geralmente referidos como filho esquerdo e filho direito.
As árvores binárias são amplamente utilizadas em algoritmos de busca, ordenação e representação hierárquica de dados.

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
Árvore Binária de Busca é um tipo especial de árvore binária onde cada nó segue a propriedade de busca:
- O valor do nó é maior que os valores de todos os nós na subárvore esquerda
- O valor do nó é menor que os valores de todos os nós na subárvore direita
- Não há valores duplicados
