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
