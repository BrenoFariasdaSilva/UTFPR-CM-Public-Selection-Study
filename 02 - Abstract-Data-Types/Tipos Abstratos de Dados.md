# Tipos abstratos de dados

## 1. Introdução

Tipos abstratos de dados (TADs) constituem um dos principais conceitos da ciência da computação porque separam a especificação lógica das operações de sua realização em memória. Essa separação permite raciocínio algorítmico, encapsulamento, substituição de implementações e manutenção evolutiva de software. Em termos formais, um TAD é definido por um conjunto de valores e por operações semanticamente válidas sobre esse conjunto, independentemente do modo como tais valores são armazenados (Horowitz; Sahni, 1986; Cormen et al., 2009).

Na prática, listas, pilhas, filas e tabelas hash ilustram diferentes comportamentos entre acesso, atualização, consumo de memória e custo de implementação. Em C, a discussão adquire profundidade maior, pois o programador controla explicitamente arranjos estáticos, alocação dinâmica, ponteiros, desalocação e organização modular em arquivos de interface e implementação. Por essa razão, o estudo de TADs em C é simultaneamente um exercício de modelagem abstrata e de implementações de baixo nível.

## 2. Fundamentação Teórica

### 2.1 Interface e implementação

A essência do TAD reside em esconder detalhes internos e expor apenas operações válidas. Em um módulo bem definido, o usuário conhece contratos como inserir, remover, buscar, empilhar ou desenfileirar, mas não depende da forma interna da estrutura. Essa separação permite trocar uma lista sequencial por uma encadeada sem alterar clientes, desde que a interface permaneça igual (Ziviani, 2004).

### 2.2 Estruturas estáticas e dinâmicas

Estruturas estáticas usam memória de tamanho fixo, normalmente baseada em vetores. São previsíveis e cache-friendly, porém limitadas em capacidade. Estruturas dinâmicas usam heap e ponteiros para crescer ou encolher em tempo de execução, ganhando flexibilidade ao custo de maior overhead, fragmentação e complexidade de gerenciamento (Sedgewick, 1998).

### 2.3 Listas, pilhas, filas e hashing

Listas são estruturas lineares utilizadas para armazenar coleções de elementos em sequência, permitindo inserções, remoções e percursos ordenados. Dependendo da implementação, podem ser baseadas em arranjos contíguos ou nós encadeados, oferecendo diferentes comportamentos entre acesso aleatório e flexibilidade de atualização.

Pilhas (*stacks*) seguem o conceito LIFO (*Last In, First Out*), na qual o último elemento inserido é o primeiro a ser removido. Essa estrutura é amplamente utilizada em chamadas recursivas, avaliação de expressões, algoritmos de retrocesso (*backtracking*) e gerenciamento de memória de execução.

Filas (*queues*) seguem o conceito FIFO (*First In, First Out*), em que o primeiro elemento inserido é o primeiro a ser removido. São empregadas em escalonamento de processos, sistemas de atendimento, buffers de comunicação e algoritmos de busca em largura (BFS).

Tabelas hash (*hash tables*) armazenam elementos por meio de uma função de dispersão (*hash function*), que transforma uma chave em uma posição de armazenamento. Quando a função hash distribui adequadamente os dados e o fator de carga permanece controlado, operações de busca, inserção e remoção apresentam custo médio próximo de $O(1)$. Em contrapartida, colisões podem ocorrer quando múltiplas chaves são mapeadas para a mesma posição, exigindo estratégias de tratamento como encadeamento separado ou endereçamento aberto (Cormen et al., 2012).

## 3. Desenvolvimento

```mermaid
flowchart LR
    A[TAD] --> B[Listas sequenciais]
    A --> C[Listas encadeadas]
    A --> D[Pilhas]
    A --> E[Filas]
    A --> F[Tabelas hash]
```

### 3.1 Listas estáticas e sequenciais

Listas sequenciais estáticas armazenam elementos em vetor contíguo. O acesso por índice é $O(1)$, mas inserções e remoções no meio exigem deslocamentos lineares.

| Estrutura      | Facilidade de implementação | Facilidade de uso | Desempenho          | Consumo de memória | Vantagens                          | Desvantagens    | Casos de uso                       | Big O principal                                |
| -------------- | --------------------------- | ----------------- | ------------------- | ------------------ | ---------------------------------- | --------------- | ---------------------------------- | ---------------------------------------------- |
| Lista estática | Alta                        | Alta              | Excelente em acesso | Baixo e previsível | Simplicidade e localidade de cache | Capacidade fixa | Tabelas pequenas, buffers estáveis | Busca O(n), acesso O(1), inserção interna O(n) |

#### Algoritmo 1: inserção ordenada em lista sequencial

**Explicação teórica.** Manter a lista ordenada reduz custo de futuras buscas binárias, mas a inserção exige localizar a posição e deslocar elementos para abrir espaço.

**Pseudocódigo**

```text
algoritmo inserir_ordenado(lista, tamanho, capacidade, valor)
    se tamanho = capacidade então retorne falso
    i <- tamanho - 1
    enquanto i >= 0 e lista[i] > valor faca
        lista[i + 1] <- lista[i]
        i <- i - 1
    lista[i + 1] <- valor
    tamanho <- tamanho + 1
    retorne verdadeiro
fim
```

**Implementação completa em C**

```c
#include <stdio.h>

#define CAPACIDADE 16

typedef struct {
    int dados[CAPACIDADE];
    int tamanho;
} ListaEstatica;

void lista_inicializar(ListaEstatica *lista) {
    lista->tamanho = 0;
}

int lista_buscar(const ListaEstatica *lista, int valor) {
    for (int indice = 0; indice < lista->tamanho; indice++) {
        if (lista->dados[indice] == valor) {
            return indice;
        }
    }
    return -1;
}

int lista_inserir_ordenado(ListaEstatica *lista, int valor) {
    if (lista->tamanho == CAPACIDADE) {
        return 0;
    }

    int indice = lista->tamanho - 1;
    while (indice >= 0 && lista->dados[indice] > valor) {
        lista->dados[indice + 1] = lista->dados[indice];
        indice--;
    }

    lista->dados[indice + 1] = valor;
    lista->tamanho++;
    return 1;
}

int lista_remover(ListaEstatica *lista, int valor) {
    int posicao = lista_buscar(lista, valor);
    if (posicao < 0) {
        return 0;
    }

    for (int indice = posicao; indice < lista->tamanho - 1; indice++) {
        lista->dados[indice] = lista->dados[indice + 1];
    }

    lista->tamanho--;
    return 1;
}
```

**Complexidade.** Busca $O(n)$; inserção e remoção no pior caso $O(n)$; acesso por índice $O(1)$; espaço $O(n)$ pré-alocado.

**Partes importantes.** O deslocamento é executado de trás para frente para não sobrescrever dados; o tamanho lógico é independente da capacidade física; a remoção reutiliza busca linear.

**Entrada e saída.** Inserindo `7, 3, 9, 5`, a lista final permanece `3 5 7 9`.

**Comparação com alternativas.** Em relação à lista encadeada, a lista estática perde em inserção no início, mas ganha em localidade de cache e simplicidade de depuração.
