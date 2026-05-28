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
