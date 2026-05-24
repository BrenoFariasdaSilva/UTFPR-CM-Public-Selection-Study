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

## Comparação

| Critério         | Matriz | Lista   |
| ---------------- | ------ | ------- |
| Espaço           | O(n²)  | O(V+E)  |
| Verificar aresta | O(1)   | O(grau) |
| Iterar vizinhos  | O(n)   | O(grau) |

---

# 4.3 Percurso em grafos (Graph Traversal)
Há dois algoritmos clássicos para percorrer grafos: BFS (Busca em Largura) e DFS (Busca em Profundidade).

## BFS (Breadth-First Search)

### Uso de recursão

```c
void bfs_recursivo(int fila[], int* ini, int* fim, int visitado[]) {
    if (*ini >= *fim)
        return;

    int v = fila[(*ini)++];

    printf("%d ", v);

    for (No* p = adj[v]; p != NULL; p = p->prox) {
        if (!visitado[p->v]) {
            visitado[p->v] = 1;
            fila[(*fim)++] = p->v;
        }
    }

    bfs_recursivo(fila, ini, fim, visitado);
}

void bfs(int inicio) {
    int visitado[100] = {0};

    int fila[100];

    int ini = 0;
    int fim = 0;

    fila[fim++] = inicio;

    visitado[inicio] = 1;

    bfs_recursivo(fila, &ini, &fim, visitado);
}
```

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

#### Estrutura básica

```text
function BFS(Graph, start):
    create empty queue Q
    for each vertex v in Graph.Vertices:
        visited[v] ← false
    visited[start] ← true
    enqueue(Q, start)

    while Q is not empty:
        u ← dequeue(Q)
        for each neighbor v of u:
            if not visited[v]:
                visited[v] ← true
                enqueue(Q, v)

    // returns visited order or reachable set as required
```

### Complexidade

O(V + E)

### Aplicações

* Menor caminho em grafos não ponderados
* Verificação de conectividade
* Níveis em árvores

---

## DFS (Depth-First Search)

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

### Uso de fila

```c
void dfs(int inicio) {
    int visitado[100] = {0};
    int pilha[100], topo = 0;

    pilha[topo++] = inicio;

    while (topo > 0) {
        int v = pilha[--topo];

        if (!visitado[v]) {
            visitado[v] = 1;
            printf("%d ", v);

            for (No* p = adj[v]; p != NULL; p = p->prox) {
                if (!visitado[p->v]) {
                    pilha[topo++] = p->v;
                }
            }
        }
    }
}
```

#### Estrutura básica

```text
function DFS_recursive(Graph, v, visited):
    visited[v] ← true
    for each neighbor u of v:
        if not visited[u]:
            DFS_recursive(Graph, u, visited)

function DFS(Graph, start):
    for each vertex v in Graph.Vertices:
        visited[v] ← false
    DFS_recursive(Graph, start, visited)

    // For full traversal, call DFS_recursive on any unvisited vertex
```

### Complexidade

O(V + E)

### Aplicações

* Detecção de ciclos
* Ordenação topológica em DAGs
* Componentes conexas

---

# 4.4 Algoritmos clássicos (Classical Algorithms)

## Caminho mínimo (Shortest Path)

Esses algoritmos são usados para encontrar menores caminhos em grafos ponderados, fundamentais em roteamento, logística e planejamento de redes.

### Dijkstra

#### Ideia

* Calcula a menor distância de um vértice origem para todos os outros
* É um algoritmo de caminho mínimo para grafos ponderados
* Muito usado em otimização de rotas
* Funciona apenas com pesos não negativos

### Restrição importante

Dijkstra NÃO funciona corretamente com arestas de peso negativo.
