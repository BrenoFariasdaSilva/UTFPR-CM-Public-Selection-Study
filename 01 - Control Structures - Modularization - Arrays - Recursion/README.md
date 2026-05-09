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
  - Pré-teste
  - Pós-teste
  - Estrutura completa
  - Uso idiomático
  - break
  - continue

## 1.2 Estruturas de repetição (Loop Structures)

- Estruturas que permitem executar blocos de código múltiplas vezes, controlando o fluxo por condições ou contadores.

### while
- Estrutura de pré-teste: avalia a condição antes de cada iteração.
- Uso: quando o número de repetições é indefinido e depende de uma condição dinâmica.
```c
while (condicao) {
  // bloco
}
```
**Vantagens:** Simples para loops dependentes de condição. Boa legibilidade.
**Desvantagens:** Risco de laço infinito se a condição nunca for falsa. Menos adequado para contadores explícitos.

### do-while
- Estrutura de pós-teste: executa o bloco ao menos uma vez, condição avaliada ao final.
- Uso: quando é necessário garantir pelo menos uma execução (ex: menus, leitura de dados).
```c
do {
  // bloco
} while (condicao);
```
**Vantagens:** Garante execução inicial. Útil para validação de entrada.
**Desvantagens:** Pode executar desnecessariamente se a condição já for falsa.
