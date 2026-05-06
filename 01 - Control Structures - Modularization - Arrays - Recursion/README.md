# 1. Estruturas de controle, modularização, vetores/matrizes e recursividade (Control Structures, Modularization, Arrays/Matrices and Recursion)

## 1.1 Estruturas de decisão (Decision Structures)
- Conceito de fluxo de controle
- if simples
  - Sintaxe em C
  - Avaliação de expressões booleanas
- if-else
  - Encadeamento
  - Problema do “dangling else”
- if-else if-else
  - Cadeias de decisão
- switch-case
  - Funcionamento interno
  - Uso com break
  - Fall-through
  - Limitações (tipos inteiros)
- Comparação entre if e switch
- Boas práticas

## 1.2 Estruturas de repetição (Loop Structures)
- Conceito de laço
- while
  - Pré-teste
- do-while
  - Pós-teste
- for
  - Estrutura completa
  - Uso idiomático
- Laços aninhados
- Controle de laço
  - break
  - continue
- Complexidade de loops (noção inicial)

## 1.3 Modularização (Modularization)
- Conceito de abstração
- Funções
  - Declaração vs definição
  - Protótipos
- Procedimentos (funções sem retorno)
- Passagem de parâmetros
  - Por valor (C padrão)
  - Simulação de passagem por referência (ponteiros)
- Escopo de variáveis
  - Local
  - Global
  - Estático
- Tempo de vida das variáveis
- Organização de código em arquivos (.c e .h)
- Reuso e coesão

## 1.4 Estruturas homogêneas (Homogeneous Data Structures)

### Vetores (arrays 1D) (Arrays)
- Definição
- Alocação estática
- Acesso por índice
- Iteração
- Operações comuns
  - Busca linear
  - Inserção
  - Remoção
- Limitações

### Matrizes (arrays 2D) (Matrices)
- Representação em memória (row-major em C)
- Acesso e travessia
- Operações clássicas
  - Soma
  - Multiplicação
- Generalização para n dimensões

## 1.5 Recursividade (Recursion)
- Definição formal
- Caso base e caso recursivo
- Pilha de chamadas
- Exemplos clássicos
  - Fatorial
  - Fibonacci
  - Torre de Hanoi
- Recursão vs iteração
- Análise de complexidade
- Problemas comuns
  - Stack overflow
- Recursão de cauda