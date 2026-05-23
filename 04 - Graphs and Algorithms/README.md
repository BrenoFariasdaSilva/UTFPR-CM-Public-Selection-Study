# Grafos e Algoritmos

# 4.1 Conceitos fundamentais (Fundamental Concepts)

## Definição de grafo

Um **grafo** é um par ordenado ( G = (V, E) ), onde:

* ( V ) é um conjunto de vértices (nós / pontos do grafo)
* E ⊆ V × V é um conjunto de arestas (conexão entre os vértices). Ou seja, “O conjunto de arestas E é um subconjunto do produto cartesiano V×V.”

---

## Tipos de grafos

### Direcionado (Directed Graph)

* Arestas possuem direção
* Representadas como pares ordenados: \( (u, v) \)
* A conexão de \(u \rightarrow v\) não implica necessariamente \(v \rightarrow u\)

#### Casos de uso

* Redes sociais (seguir alguém no Instagram/Twitter)
* Fluxo de páginas web (hiperlinks)
* Sistemas de dependência
* Fluxos de processamento
* Rotas com sentido único

---

### Não-direcionado (Undirected Graph)

* Arestas não possuem direção (bidirecionais)
* Representadas como pares não ordenados: \( \{u, v\} \)
* Se existe conexão entre \(u\) e \(v\), ambos podem se alcançar diretamente

#### Casos de uso

* Redes de amizade
* Conexões físicas entre computadores
* Redes elétricas
* Mapas com ruas de mão dupla
* Ligações entre componentes conectados mutuamente

---

### Ponderado (Weighted Graph)

* Arestas possuem peso/custo associado
* O peso pode representar distância, custo, tempo, capacidade ou prioridade

#### Casos de uso

* GPS e cálculo de rotas
* Redes de transporte
* Redes de computadores com latência
* Algoritmos de caminho mínimo
* Sistemas logísticos

---

### Não ponderado (Unweighted Graph)

* Todas as arestas têm peso igual (ou irrelevante)
* O interesse principal é apenas a existência da conexão

#### Casos de uso

* Redes sociais simples
* Verificação de conectividade
* Busca em largura (BFS)
* Jogos e mapas simples
* Descoberta de componentes conectados

---

### DAG (Directed Acyclic Graph)

* É um grafo direcionado sem ciclos. Um ciclo ocorre quando há um caminho orientado que começa e termina no mesmo vértice. Em um DAG, isso não é permitido.
* Não existe caminho orientado que saia de um vértice e volte para ele mesmo
* Muito usado em dependências, pré-requisitos e ordenação topológica

#### Casos de uso

* Pipelines de processamento
* Compiladores
* Sistemas de build
* Dependências de pacotes
* Fluxos de tarefas
* Agendamento de execução
* Versionamento e histórico de commits

---

# 4.2 Representação (Graph Representation)
Há duas formas comuns de representar grafos em memória:

## Matriz de adjacência

### Definição

Matriz ( N x N ), onde:

```text
M[i][j] = 1 se existe aresta entre i e j
```

### Exemplo em C

```c
int G[100][100];
```

### Vantagens

* Acesso O(1) para verificar arestas
* Simples implementação

### Desvantagens

* Consome O(n²) memória
* Ineficiente para grafos esparsos

---

## Lista de adjacência

### Definição

Cada vértice possui uma lista de vizinhos

### Estrutura em C

```c
typedef struct No {
    int v;
    struct No* prox;
} No;

No* adj[100];
```

### Vantagens

* Usa O(V + E) memória
* Eficiente para grafos esparsos

### Desvantagens

* Acesso mais lento para verificar aresta

---
