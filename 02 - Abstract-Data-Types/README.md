
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
## Implementação Dinâmica (lista encadeada)
```c
typedef struct No {
    int valor;
    struct No* prox;
} No;
No* inicio = NULL;
No* fim = NULL;
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
- **Encadeamento externo:** cada posição da tabela aponta para uma lista encadeada (dinâmica) de elementos
- **Endereçamento aberto:** elementos colidem e são realocados em outras posições do próprio array (estático)

## Fator de carga
α = n / m

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
