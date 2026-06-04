# Algoritmos de Busca e Ordenação

*(Searching and Sorting Algorithms)*

---

# 5.1 Algoritmos de busca (Searching Algorithms)

## Busca linear (Linear Search)

### Funcionamento

Percorre o vetor sequencialmente até encontrar o elemento ou chegar ao final.

---

### Implementação em C

```c
int busca_linear(int v[], int n, int x) {
    for (int i = 0; i < n; i++) {
        if (v[i] == x)
            return i;
    }
    return -1;
}
```

### Complexidade

| Caso   | Complexidade |
| ------ | ------------ |
| Melhor | O(1)         |
| Médio  | O(n)         |
| Pior   | O(n)         |

### Observações

* Não requer ordenação
* Simples, mas ineficiente para grandes volumes

---

## Busca binária (Binary Search)

### Pré-requisito

Vetor deve estar ordenado

### Funcionamento

Divide o espaço de busca pela metade a cada iteração.

---

### Implementação iterativa

```c
int busca_binaria(int v[], int n, int x) {
    int ini = 0, fim = n - 1;

    while (ini <= fim) {
        int meio = (ini + fim) / 2;

        if (v[meio] == x)
            return meio;
        else if (x < v[meio])
            fim = meio - 1;
        else
            ini = meio + 1;
    }
    return -1;
}
```

---

### Implementação recursiva

```c
int busca_binaria_rec(int v[], int ini, int fim, int x) {
    if (ini > fim) return -1;

    int meio = (ini + fim) / 2;

    if (v[meio] == x) return meio;
    if (x < v[meio])
        return busca_binaria_rec(v, ini, meio - 1, x);
    return busca_binaria_rec(v, meio + 1, fim, x);
}
```

### Complexidade

| Caso   | Complexidade |
| ------ | ------------ |
| Melhor | O(1)         |
| Médio  | O(log n)     |
| Pior   | O(log n)     |

---

# 5.2 Algoritmos de ordenação (Sorting Algorithms)

## Simples — O(n²)

### Bubble Sort

#### Funcionamento

* Compara elementos adjacentes
* Troca se estiverem fora de ordem
* Repete até não haver trocas

#### Implementação

```c
void bubble_sort(int v[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (v[j] > v[j+1]) {
                int temp = v[j];
                v[j] = v[j+1];
                v[j+1] = temp;
            }
        }
    }
}
```

#### Complexidade

O(n²)

---

### Selection Sort

#### Funcionamento

* Seleciona o menor elemento
* Coloca na posição correta

#### Implementação

```c
void selection_sort(int v[], int n) {
    for (int i = 0; i < n-1; i++) {
        int min = i;
        for (int j = i+1; j < n; j++) {
            if (v[j] < v[min])
                min = j;
        }
        int temp = v[i];
        v[i] = v[min];
        v[min] = temp;
    }
}
```

#### Complexidade

O(n²)

---

### Insertion Sort

#### Funcionamento

* Insere cada elemento na posição correta
* Similar a ordenar cartas

#### Implementação

```c
void insertion_sort(int v[], int n) {
    for (int i = 1; i < n; i++) {
        int chave = v[i];
        int j = i - 1;

        while (j >= 0 && v[j] > chave) {
            v[j+1] = v[j];
            j--;
        }
        v[j+1] = chave;
    }
}
```

### Complexidade

| Caso   | Complexidade |
| ------ | ------------ |
| Melhor | O(n)         |
| Médio  | O(n²)        |
| Pior   | O(n²)        |

#### Estabilidade

Estável

---

## Eficientes — O(n log n)

### Merge Sort

#### Ideia (Divisão e conquista)

* Divide o vetor em duas partes
* Ordena recursivamente
* Combina (merge)

#### Implementação

```c
void merge(int v[], int l, int m, int r) {
    int i = l, j = m+1, k = 0;
    int temp[1000];

    while (i <= m && j <= r) {
        if (v[i] <= v[j]) temp[k++] = v[i++];
        else temp[k++] = v[j++];
    }

    while (i <= m) temp[k++] = v[i++];
    while (j <= r) temp[k++] = v[j++];

    for (i = l, k = 0; i <= r; i++, k++)
        v[i] = temp[k];
}

void merge_sort(int v[], int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        merge_sort(v, l, m);
        merge_sort(v, m+1, r);
        merge(v, l, m, r);
    }
}
```

#### Complexidade

O(n log n)

#### Estabilidade

Estável

#### Memória

Usa memória extra

---

### Quick Sort

#### Ideia

* Escolhe pivô
* Particiona em menores e maiores
* Ordena recursivamente

#### Implementação

```c
int particiona(int v[], int l, int r) {
    int pivo = v[r];
    int i = l - 1;

    for (int j = l; j < r; j++) {
        if (v[j] < pivo) {
            i++;
            int temp = v[i];
            v[i] = v[j];
            v[j] = temp;
        }
    }

    int temp = v[i+1];
    v[i+1] = v[r];
    v[r] = temp;

    return i+1;
}

void quick_sort(int v[], int l, int r) {
    if (l < r) {
        int p = particiona(v, l, r);
        quick_sort(v, l, p-1);
        quick_sort(v, p+1, r);
    }
}
```

### Complexidade

| Caso   | Complexidade |
| ------ | ------------ |
| Melhor | O(n log n)   |
| Médio  | O(n log n)   |
| Pior   | O(n²)        |

#### Estabilidade

Não estável

---

### Heap Sort

#### Ideia

* Usa heap binário. Uma heap é uma estrutura de dados que mantém a propriedade de heap: cada nó é maior (max-heap) ou menor (min-heap) que seus filhos.
* Extrai maior elemento repetidamente

#### Heapify

```c
void heapify(int v[], int n, int i) {
    int maior = i;
    int esq = 2*i + 1;
    int dir = 2*i + 2;

    if (esq < n && v[esq] > v[maior])
        maior = esq;

    if (dir < n && v[dir] > v[maior])
        maior = dir;

    if (maior != i) {
        int temp = v[i];
        v[i] = v[maior];
        v[maior] = temp;

        heapify(v, n, maior);
    }
}
```

#### Construção + ordenação

```c
void heap_sort(int v[], int n) {
    for (int i = n/2 - 1; i >= 0; i--)
        heapify(v, n, i);

    for (int i = n-1; i > 0; i--) {
        int temp = v[0];
        v[0] = v[i];
        v[i] = temp;

        heapify(v, i, 0);
    }
}
```

#### Complexidade

O(n log n)

#### Estabilidade

Não estável

---

# 5.3 Comparações importantes (Important Comparisons)

## Estáveis vs Instáveis

| Algoritmo | Estável |
| --------- | ------- |
| Bubble    | Sim     |
| Selection | Não     |
| Insertion | Sim     |
| Merge     | Sim     |
| Quick     | Não     |
| Heap      | Não     |

---

## In-place vs Não in-place

| Algoritmo | In-place |
| --------- | -------- |
| Bubble    | Sim      |
| Selection | Sim      |
| Insertion | Sim      |
| Merge     | Não      |
| Quick     | Sim      |
| Heap      | Sim      |

---
