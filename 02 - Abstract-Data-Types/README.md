
# Tipos Abstratos de Dados (TADs)
*(Abstract Data Types - ADTs)*

---

# 2.0 Visão Geral: Estruturas Estáticas vs. Dinâmicas

Em estruturas de dados, **estático** significa tamanho fixo e alocação em tempo de compilação (ex: arrays), enquanto **dinâmico** permite crescimento/redução em tempo de execução (ex: listas encadeadas, realloc, malloc/free).

| Tipo     | Alocação                            | Tamanho  | Vantagens                         | Desvantagens                        |
| -------- | ----------------------------------- | -------- | --------------------------------- | ----------------------------------- |
| Estático | Em tempo de compilação (stack/data) | Fixo     | Simples, rápido, sem fragmentação | Limite fixo, desperdício de memória |
| Dinâmico | Em tempo de execução (heap)         | Variável | Flexível, cresce conforme uso     | Mais complexo, risco de vazamento   |

---

# 2.1 Conceito de TAD (ADT Concept)

## Definição formal
Um **Tipo Abstrato de Dados (TAD)** é uma especificação matemática de um conjunto de dados e das operações permitidas sobre esses dados, independentemente de sua implementação.

---

## Definição
FIFO (First In, First Out)



## Implementação Estática (vetor circular)
```c
int fila[100];
int inicio = 0, fim = 0;
```
### Operações
- **enqueue:**
```c
int enqueue(int x) {
    if ((fim + 1) % 100 == inicio) return 0; // cheia
    fila[fim] = x;
    fim = (fim + 1) % 100;
    return 1;
}
```
- **dequeue:**
```c
int dequeue() {
    if (inicio == fim) return -1; // vazia
    int v = fila[inicio];
    inicio = (inicio + 1) % 100;
    return v;
}
```

## Implementação Dinâmica (lista encadeada)
```c
typedef struct No {
    int valor;
    struct No* prox;
} No;
No* inicio = NULL;
No* fim = NULL;
```
### Operações
- **enqueue:**
```c
void enqueue(int x) {
    No* novo = malloc(sizeof(No));
    novo->valor = x;
    novo->prox = NULL;
    if (!fim) {
        inicio = fim = novo;
    } else {
        fim->prox = novo;
        fim = novo;
    }
}
```
- **dequeue:**
```c
int dequeue() {
    if (!inicio) return -1;
    int v = inicio->valor;
    No* temp = inicio;
    inicio = inicio->prox;
    if (!inicio) fim = NULL;
    free(temp);
    return v;
}
```

---


# 2.5 Tabelas Hash (Hash Tables)


## Função hash
```c
int hash(int chave) {
    return chave % TAM;
}
```

## Operações principais
- **Inserção (endereçamento aberto):**
```c
int inserir(int t[], int chave) {
    int h = hash(chave);
    for (int i = 0; i < TAM; i++) {
        int pos = (h + i) % TAM;
        if (t[pos] == 0) { t[pos] = chave; return 1; }
    }
    return 0; // tabela cheia
}
```
- **Busca (endereçamento aberto):**
```c
int buscar(int t[], int chave) {
    int h = hash(chave);
    for (int i = 0; i < TAM; i++) {
        int pos = (h + i) % TAM;
        if (t[pos] == 0) return 0;
        if (t[pos] == chave) return 1;
    }
    return 0;
}
```
- **Inserção (encadeamento externo):**
```c
typedef struct No {
    int chave;
    struct No* prox;
} No;
No* tabela[TAM];

void inserir(No* tabela[], int chave) {
    int h = hash(chave);
    No* novo = malloc(sizeof(No));
    novo->chave = chave;
    novo->prox = tabela[h];
    tabela[h] = novo;
}
```
- **Busca (encadeamento externo):**
```c
int buscar(No* tabela[], int chave) {
    int h = hash(chave);
    for (No* p = tabela[h]; p; p = p->prox)
        if (p->chave == chave) return 1;
    return 0;
}
```

## Métodos de tratamento de colisão
- **Encadeamento externo:** cada posição da tabela aponta para uma lista encadeada (dinâmica) de elementos. Vantagem: sem limite rígido de ocupação por posição.
- **Endereçamento aberto:** elementos colidem e são realocados em outras posições do próprio array (estático). Vantagem: não usa ponteiros, mas pode degradar se a tabela ficar cheia.


## Fator de carga
α = n / m (n = número de elementos, m = tamanho da tabela)


## Complexidade
- Médio: O(1)  
- Pior caso: O(n)  

---


# COMPARAÇÕES IMPORTANTES

| Estrutura                   | Acesso | Inserção | Remoção | Alocação |
| --------------------------- | ------ | -------- | ------- | -------- |
| Array Estático              | O(1)   | O(n)     | O(n)    | Estática |
| Array Dinâmico              | O(1)   | O(n)     | O(n)    | Dinâmica |
| Lista Encadeada             | O(n)   | O(1)     | O(1)    | Dinâmica |
| Pilha Estática              | O(1)   | O(1)     | O(1)    | Estática |
| Pilha Dinâmica              | O(1)   | O(1)     | O(1)    | Dinâmica |
| Fila Estática               | O(1)   | O(1)     | O(1)    | Estática |
| Fila Dinâmica               | O(1)   | O(1)     | O(1)    | Dinâmica |
| Hash (encadeada)            | O(1)   | O(1)     | O(1)    | Dinâmica |
| Hash (endereçamento aberto) | O(1)   | O(1)     | O(1)    | Estática |

---


# COMO ISSO CAI NA PROVA


Você precisa:
- Definir TAD e explicar diferença entre estático e dinâmico
- Comparar vantagens e desvantagens de cada abordagem
- Explicar colisões e métodos de resolução
- Implementar versões estáticas e dinâmicas em C
- Analisar complexidade e uso de memória

---

# CONCLUSÃO

Domínio esperado:
- Implementação em C (estático e dinâmico)
- Comparação teórica e prática
- Entendimento de complexidade e uso de memória
