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
