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
