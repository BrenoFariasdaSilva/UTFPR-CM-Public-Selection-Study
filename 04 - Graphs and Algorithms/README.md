# Grafos e Algoritmos

*(Graphs and Algorithms)*

---

# 4.1 Conceitos fundamentais (Fundamental Concepts)

## Definição de grafo

Um **grafo** é um par ordenado ( G = (V, E) ), onde:

* ( V ) é um conjunto de vértices (nós)
* ( E \subseteq V \times V ) é um conjunto de arestas (conexões)

---

## Tipos de grafos

### Direcionado (Directed Graph)

* Arestas possuem direção
* Representadas como pares ordenados: ( (u, v) )

### Não-direcionado (Undirected Graph)

* Arestas não possuem direção
* Representadas como pares não ordenados: ( {u, v} )

---

### Ponderado (Weighted Graph)

* Arestas possuem peso/custo associado

### Não ponderado (Unweighted Graph)

* Todas as arestas têm peso igual (ou irrelevante)

---

# 4.2 Representação (Graph Representation)

## Matriz de adjacência

### Definição

Matriz ( n \times n ), onde:

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

## Comparação

| Critério         | Matriz | Lista   |
| ---------------- | ------ | ------- |
| Espaço           | O(n²)  | O(V+E)  |
| Verificar aresta | O(1)   | O(grau) |
| Iterar vizinhos  | O(n)   | O(grau) |

---

# 4.3 Percurso em grafos (Graph Traversal)

## BFS (Breadth-First Search)

### Ideia

Explora o grafo por níveis (camadas)

### Uso de fila

```c
void bfs(int inicio) {
    int visitado[100] = {0};
    int fila[100], ini = 0, fim = 0;

    fila[fim++] = inicio;
    visitado[inicio] = 1;

    while (ini < fim) {
        int v = fila[ini++];
        printf("%d ", v);

        for (No* p = adj[v]; p != NULL; p = p->prox) {
            if (!visitado[p->v]) {
                visitado[p->v] = 1;
                fila[fim++] = p->v;
            }
        }
    }
}
```

### Complexidade

O(V + E)

### Aplicações

* Menor caminho em grafos não ponderados
* Verificação de conectividade
* Níveis em árvores

---

## DFS (Depth-First Search)

### Ideia

Explora profundamente antes de retroceder

### Uso de recursão

```c
void dfs(int v, int visitado[]) {
    visitado[v] = 1;
    printf("%d ", v);

    for (No* p = adj[v]; p != NULL; p = p->prox) {
        if (!visitado[p->v])
            dfs(p->v, visitado);
    }
}
```

### Complexidade

O(V + E)

### Aplicações

* Detecção de ciclos
* Ordenação topológica
* Componentes conexas

---

# 4.4 Algoritmos clássicos (Classical Algorithms)

## Caminho mínimo (Shortest Path)

### Dijkstra

#### Ideia

* Calcula a menor distância de um vértice origem para todos os outros
* Funciona apenas com pesos não negativos

#### Estrutura básica

```c
#define INF 999999

void dijkstra(int G[100][100], int n, int origem) {
    int dist[100], visitado[100] = {0};

    for (int i = 0; i < n; i++)
        dist[i] = INF;

    dist[origem] = 0;

    for (int i = 0; i < n; i++) {
        int u = -1;

        for (int j = 0; j < n; j++)
            if (!visitado[j] && (u == -1 || dist[j] < dist[u]))
                u = j;

        visitado[u] = 1;

        for (int v = 0; v < n; v++) {
            if (G[u][v] && dist[u] + G[u][v] < dist[v])
                dist[v] = dist[u] + G[u][v];
        }
    }
}
```

### Complexidade

* O(V²) (implementação simples)
* O((V + E) log V) com heap

---

## Árvores Geradoras Mínimas (MST)

### Kruskal

#### Ideia

* Ordena arestas por peso
* Adiciona arestas sem formar ciclo

#### Estrutura

* Usa Union-Find (conjuntos disjuntos)

#### Complexidade

O(E log E)

---

### Prim

#### Ideia

* Cresce a árvore a partir de um vértice
* Sempre adiciona a menor aresta possível

#### Complexidade

* O(V²) ou O((V + E) log V)

---

# 4.5 Propriedades (Graph Properties)

## Conectividade

### Grafo conectado

Existe caminho entre todos os pares de vértices

### Componentes conexas

Subgrafos conectados

* DFS/BFS identificam componentes

---

## Ciclos

### Definição

Caminho que começa e termina no mesmo vértice

### Detecção

DFS com controle de visita

---

# COMPARAÇÕES IMPORTANTES

| Algoritmo | Estrutura       | Complexidade       |
| --------- | --------------- | ------------------ |
| BFS       | Fila            | O(V+E)             |
| DFS       | Pilha/Recursão  | O(V+E)             |
| Dijkstra  | Grafo ponderado | O(V²) / O(E log V) |
| Kruskal   | MST             | O(E log E)         |
| Prim      | MST             | O(V²) / O(E log V) |

---

# COMO ISSO CAI NA PROVA

Você precisa:

* Definir formalmente grafos
* Comparar representações (matriz vs lista)
* Explicar BFS e DFS passo a passo
* Implementar BFS/DFS em C
* Explicar Dijkstra (restrições e funcionamento)
* Diferenciar Kruskal vs Prim
* Identificar conectividade e ciclos

---

# CONCLUSÃO

Grafos são fundamentais para:

* Redes
* Caminhos mínimos
* Estruturas complexas

### Domínio esperado:

* Implementação básica em C
* Clareza conceitual
* Capacidade de análise de complexidade
