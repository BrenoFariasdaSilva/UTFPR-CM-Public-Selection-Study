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
