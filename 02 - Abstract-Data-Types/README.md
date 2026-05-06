# Tipos Abstratos de Dados (TADs)  
*(Abstract Data Types - ADTs)*

---

# 2.1 Conceito de TAD (ADT Concept)

## Definição formal
Um **Tipo Abstrato de Dados (TAD)** é uma especificação matemática de um conjunto de dados e das operações permitidas sobre esses dados, independentemente de sua implementação.

---

## Separação entre interface e implementação
- **Interface:** define *o que* o TAD faz  
- **Implementação:** define *como* o TAD faz  

### Exemplo
```c
// Interface (lista.h)
void inserir(int x);
int remover(int x);

// Implementação (lista.c)
```

## Encapsulamento
- Oculta detalhes internos  
- Garante integridade dos dados  
- Permite troca de implementação  

---

# 2.2 Listas (Lists)

## Lista sequencial
```c
typedef struct {
    int dados[100];
    int tamanho;
} Lista;
```

### Complexidade
- Inserção: O(n)  
- Remoção: O(n)  
- Busca: O(n)  

---

## Lista encadeada

### Estrutura de nó
```c
typedef struct No {
    int valor;
    struct No* prox;
} No;
```

### Inserção no início
```c
No* inserir_inicio(No* head, int x) {
    No* novo = malloc(sizeof(No));
    novo->valor = x;
    novo->prox = head;
    return novo;
}
```

### Percurso
```c
for (No* p = head; p != NULL; p = p->prox)
    printf("%d\n", p->valor);
```

---

## Lista duplamente encadeada
```c
typedef struct No {
    int valor;
    struct No* prox;
    struct No* ant;
} No;
```

---

## Lista circular
- Último aponta para o primeiro  
- Não possui NULL  

---

# 2.3 Pilhas (Stacks)

## Definição
LIFO (Last In, First Out)

## Implementação
```c
int pilha[100];
int topo = -1;
```

## Operações
- push  
- pop  
- top  

## Complexidade
- O(1)

---

# 2.4 Filas (Queues)

## Definição
FIFO (First In, First Out)

## Vetor circular
```c
int fila[100];
int inicio = 0, fim = 0;
```

## Operações
- enqueue  
- dequeue  

---

# 2.5 Tabelas Hash (Hash Tables)

## Função hash
```c
int hash(int chave) {
    return chave % TAM;
}
```

## Colisões
- Encadeamento  
- Endereçamento aberto  

## Fator de carga
α = n / m

## Complexidade
- Médio: O(1)  
- Pior caso: O(n)  

---

# COMPARAÇÕES IMPORTANTES

| Estrutura | Acesso | Inserção | Remoção |
|----------|--------|----------|--------|
| Array | O(1) | O(n) | O(n) |
| Lista | O(n) | O(1) | O(1) |
| Hash | O(1) | O(1) | O(1) |

---

# COMO ISSO CAI NA PROVA

Você precisa:
- Definir TAD  
- Comparar estruturas  
- Explicar colisões  
- Implementar em C  
- Analisar complexidade  

---

# CONCLUSÃO

Domínio esperado:
- Implementação em C  
- Comparação teórica  
- Entendimento de complexidade  
