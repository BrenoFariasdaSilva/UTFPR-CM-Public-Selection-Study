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

### for
- Estrutura compacta para laços com contador explícito: inicialização, condição e incremento em uma linha.
- Uso: quando o número de iterações é conhecido ou controlado por variável.
```c
for (int i = 0; i < n; i++) {
  // bloco
}
```
**Vantagens:** Sintaxe clara para laços contados. Fácil de ler e manter.
**Desvantagens:** Menos flexível para condições complexas ou múltiplos contadores.

### Laços aninhados (Nested Loops)
- Um loop dentro de outro. Usados para percorrer estruturas multidimensionais (ex: matrizes).
```c
for (int i = 0; i < n; i++) {
  for (int j = 0; j < m; j++) {
    // bloco
  }
}
```
**Atenção:** O número total de iterações é multiplicativo (n × m).

### break e continue
- `break`: interrompe imediatamente apenas o loop mais interno em execução.
- `continue`: pula para a próxima iteração do loop mais interno.

**Exemplo: break em laço aninhado**
```c
for (int i = 0; i < 3; i++) {
  for (int j = 0; j < 3; j++) {
    if (j == 1) break; // sai apenas do for interno
    printf("%d %d\n", i, j);
  }
}
```

**Exemplo: continue em laço aninhado**
```c
for (int i = 0; i < 3; i++) {
  for (int j = 0; j < 3; j++) {
    if (j == 1) continue; // pula apenas a iteração do for interno
    printf("%d %d\n", i, j);
  }
}
```

**Comportamento em laços aninhados:**
- `break` e `continue` afetam somente o loop mais interno onde estão inseridos.
- Para sair de múltiplos níveis, é necessário lógica adicional (ex: flags, goto).
- Erros comuns: esperar que `break`/`continue` afetem todos os níveis.

### Complexidade de loops
- Um único loop sobre n elementos: O(n)
- Dois loops aninhados: O(n²)
- Três loops aninhados: O(n³)
- Cada nível adicional multiplica o número total de iterações.
- Exemplo: para matriz n × m, total de iterações = n × m (O(nm)).

---

## goto (desvio incondicional de fluxo)

O comando `goto` em C realiza um salto incondicional para um rótulo (label) definido no código.

**Sintaxe mínima:**
```c
goto rotulo;

rotulo:
  // destino
```

- O rótulo é um identificador seguido de dois pontos.
- O fluxo de execução salta diretamente para o rótulo, ignorando código intermediário.

**Exemplo: simulação de repetição**
```c
int i = 0;
inicio:
  if (i < 5) {
    printf("%d\n", i);
    i++;
    goto inicio;
  }
```

**Por que goto prejudica a programação estruturada:**
- Quebra o fluxo linear, dificulta leitura e manutenção.
- Facilita o surgimento de "código espaguete" (spaghetti code).

**Contexto histórico:**
- Muito usado em C antigo e programação de sistemas (décadas de 1970/80).
- Ainda válido no padrão C moderno, mas fortemente desencorajado.
- Praticamente obsoleto após a adoção dos princípios de programação estruturada.

**Casos raros de uso válido:**
- Centralização de limpeza de recursos (cleanup).
- Tratamento de erro em código de baixo nível/sistemas.

---

## 1.3 Modularização (Modularization)
  - Declaração vs definição
  - Protótipos
  - Por valor (C padrão)
  - Simulação de passagem por referência (ponteiros)
  - Local
  - Global
  - Estático

## 1.3 Modularização (Modularization)

- Modularização consiste em dividir o programa em funções/módulos independentes, cada um com responsabilidade única.
- Funções facilitam manutenção, reuso e testes.
- Código modular reduz acoplamento e aumenta coesão.

### Relação com SOLID
- **SRP (Single Responsibility Principle):** cada função deve ter um único propósito, facilitando manutenção e testes.
- **OCP (Open/Closed Principle):** módulos/funções devem ser abertos para extensão, mas fechados para modificação. Novos comportamentos devem ser adicionados por novas funções/módulos, sem alterar código estável. Em C, isso é obtido separando funções em arquivos e headers, permitindo extensão sem reescrever implementações existentes.

- Organização em arquivos `.c` (implementação) e `.h` (interface) reforça modularidade e encapsulamento.

---


- Operações comuns
  - Busca linear
  - Inserção

## 1.4 Estruturas homogêneas (Homogeneous Data Structures)

### Vetores (arrays 1D) (Arrays)
- Estruturas de dados homogêneas de tamanho fixo, armazenadas em posições contíguas de memória.
- Acesso por índice: O(1).
- Passagem para funções: arrays decaem para ponteiros (`int v[]` ≡ `int *v`), permitindo que alterações na função afetem o array original.
```c
void altera(int v[], int n) { v[0] = 99; } // afeta o array original
```
- Limitações: tamanho fixo, não há verificação de limites.

### Matrizes (arrays 2D) (Matrices)
- Representadas como arrays de arrays: `int m[LIN][COL]`.
- Passagem para funções: é obrigatório informar o número de colunas (`void f(int m[][COL], int lin)`), pois a aritmética de deslocamento depende desse valor.
- Relação array/ponteiro: `m[i][j]` é equivalente a `*(&m[0][0] + i*COL + j)`.
- **Layout em memória:** C usa ordem row-major: linhas armazenadas sequencialmente.
- **Cálculo de endereço:**
  - `endereço = base + ((i * num_colunas) + j)`
- **Eficiência:** Percorrer por linhas é mais eficiente devido à localidade de cache.
```c
for (int i = 0; i < LIN; i++)
  for (int j = 0; j < COL; j++)
    m[i][j] = ...;
```
- Generalização para n dimensões: sintaxe e aritmética análogas.

---
- Limitações

### Matrizes (arrays 2D) (Matrices)
- Representação em memória (row-major em C)
- Acesso e travessia
- Operações clássicas
  - Soma
  - Multiplicação
- Generalização para n dimensões

## 1.5 Recursividade (Recursion)

- Técnica em que uma função chama a si mesma para resolver subproblemas menores.

### Definição formal
- Uma função recursiva é definida por:
  - **Caso base:** condição que encerra a recursão (sem chamada recursiva).
  - **Caso recursivo:** chamada da função para um subproblema mais simples.

### Pilha de chamadas
- Cada chamada recursiva é empilhada até atingir o caso base.
- O retorno ocorre em ordem inversa (LIFO), desempilhando as chamadas.

---

### Exemplos clássicos

#### Fatorial
```c
int fatorial(int n) {
    if (n == 0) return 1; // caso base
    return n * fatorial(n - 1); // caso recursivo
}
```
**Trace para fatorial(4):**
```
fatorial(4)
  → 4 * fatorial(3)
      → 3 * fatorial(2)
          → 2 * fatorial(1)
              → 1 * fatorial(0)
                  → 1
```
Resultado: 24

#### Fibonacci
```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```
**Trace para fib(4):**
```
fib(4)
  → fib(3) + fib(2)
      → (fib(2) + fib(1)) + (fib(1) + fib(0))
```
Resultado: 3

#### Torre de Hanoi
```c
void hanoi(int n, char A, char B, char C) {
    if (n > 0) {
        hanoi(n-1, A, C, B);
        printf("Move disco %d de %c para %c\n", n, A, C);
        hanoi(n-1, B, A, C);
    }
}
```

---

### Recursão vs iteração
| Aspecto        | Recursão                       | Iteração                        |
| -------------- | ------------------------------ | ------------------------------- |
| Legibilidade   | Alta para problemas recursivos | Alta para laços simples         |
| Desempenho     | Overhead de chamadas de função | Geralmente mais eficiente       |
| Uso de memória | O(n) na pilha                  | O(1) tipicamente                |
| Quando usar    | Árvores, divisão e conquista   | Sequências lineares, contadores |

---

### Análise de complexidade
- Cada chamada recursiva consome espaço na pilha de execução.
- Exemplo:
  - Fatorial: O(n) tempo, O(n) espaço (n chamadas empilhadas)
  - Fibonacci: O(2^n) tempo (sem otimização), O(n) espaço
  - Torre de Hanoi: O(2^n) movimentos

---

### Problemas comuns
- **Stack overflow:** ocorre quando a recursão é muito profunda ou não há caso base correto.
- **Repetição desnecessária:** recursão ingênua pode recalcular subproblemas (ex: Fibonacci sem memoização).

---
