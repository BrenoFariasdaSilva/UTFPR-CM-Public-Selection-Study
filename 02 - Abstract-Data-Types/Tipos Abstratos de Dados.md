# Tipos abstratos de dados

## 1. Introdução

Tipos abstratos de dados (TADs) constituem um dos principais conceitos da ciência da computação porque separam a especificação lógica das operações de sua realização em memória. Essa separação permite raciocínio algorítmico, encapsulamento, substituição de implementações e manutenção evolutiva de software. Em termos formais, um TAD é definido por um conjunto de valores e por operações semanticamente válidas sobre esse conjunto, independentemente do modo como tais valores são armazenados (Horowitz; Sahni, 1986; Cormen et al., 2009).

Na prática, listas, pilhas, filas e tabelas hash ilustram diferentes comportamentos entre acesso, atualização, consumo de memória e custo de implementação. Em C, a discussão adquire profundidade maior, pois o programador controla explicitamente arranjos estáticos, alocação dinâmica, ponteiros, desalocação e organização modular em arquivos de interface e implementação. Por essa razão, o estudo de TADs em C é simultaneamente um exercício de modelagem abstrata e de implementações de baixo nível.

## 2. Fundamentação Teórica

### 2.1 Interface e implementação

A essência do TAD reside em esconder detalhes internos e expor apenas operações válidas. Em um módulo bem definido, o usuário conhece contratos como inserir, remover, buscar, empilhar ou desenfileirar, mas não depende da forma interna da estrutura. Essa separação permite trocar uma lista sequencial por uma encadeada sem alterar clientes, desde que a interface permaneça igual (Ziviani, 2004).
