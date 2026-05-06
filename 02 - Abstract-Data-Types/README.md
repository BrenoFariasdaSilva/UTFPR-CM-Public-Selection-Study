# 2. Tipos Abstratos de Dados (TADs) (Abstract Data Types - ADTs)

## 2.1 Conceito de TAD (ADT Concept)
- Separação entre interface e implementação
- Encapsulamento
- Especificação formal de operações

## 2.2 Listas (Lists)

### Listas sequenciais (array-based) (Sequential Lists)
- Estrutura
- Operações
  - Inserção
  - Remoção
  - Busca
- Vantagens e desvantagens

### Listas encadeadas (Linked Lists)

#### Lista simplesmente encadeada (Singly Linked List)
- Estrutura de nó
- Inserção (início, meio, fim)
- Remoção
- Percurso
- Complexidade

#### Lista duplamente encadeada (Doubly Linked List)
- Ponteiros duplos
- Inserção/remoção mais eficientes

#### Lista circular (Circular List)
- Características
- Aplicações

## 2.3 Pilhas (Stacks)
- Definição (LIFO)
- Operações
  - push
  - pop
  - top
- Implementação
  - Vetor
  - Lista encadeada
- Aplicações
  - Avaliação de expressões
  - Backtracking
- Análise de complexidade

## 2.4 Filas (Queues)
- Definição (FIFO)
- Operações
  - enqueue
  - dequeue
- Implementações
  - Vetor (circular)
  - Lista encadeada
- Variações
  - Deque
  - Fila de prioridade (Priority Queue - conceito)

## 2.5 Tabelas Hash (Hash Tables)
- Função hash
- Colisões
- Métodos de resolução
  - Encadeamento (chaining)
  - Endereçamento aberto (open addressing)
    - Linear probing
    - Quadratic probing
    - Double hashing
- Fator de carga
- Rehashing
- Complexidade média vs pior caso
