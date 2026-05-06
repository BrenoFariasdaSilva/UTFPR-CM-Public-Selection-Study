# Estruturas de Controle, Modularização, Vetores/Matrizes e Recursividade  
*(Control Structures, Modularization, Arrays/Matrices and Recursion)*

---

# 1.1 Estruturas de decisão (Decision Structures)

## Conceito de fluxo de controle
Fluxo de controle define a ordem de execução das instruções em um programa. Em C, por padrão, a execução é sequencial, mas pode ser alterada por estruturas de decisão e repetição.

---

## if simples

### Sintaxe em C
```c
if (condicao) {
    // bloco de código
}
```

### Avaliação de expressões booleanas
Em C, qualquer valor diferente de 0 é considerado verdadeiro.  
O valor 0 é considerado falso.

```c
int x = 10;
if (x) {
    printf("Verdadeiro\n");
}
```

## if-else
```c
if (condicao) {
    // verdadeiro
} else {
    // falso
}
```

### Encadeamento
```c
if (x > 0) {
    printf("Positivo");
} else {
    printf("Não positivo");
}
```

### Problema do “dangling else”
Ambiguidade na associação do else:

```c
if (a > b)
    if (a > c)
        printf("A");
    else
        printf("B");
```

O else associa-se ao if mais próximo.

## if-else if-else
```c
if (x > 0) {
    printf("Positivo");
} else if (x < 0) {
    printf("Negativo");
} else {
    printf("Zero");
}
```

## switch-case

### Sintaxe
```c
switch (expressao) {
    case 1:
        // código
        break;
    case 2:
        // código
        break;
    default:
        // código
}
```

### Observações
- Usa apenas tipos inteiros
- Pode ser mais eficiente que múltiplos if
- Uso de `break` evita execução em cascata

### Fall-through
```c
case 1:
case 2:
    printf("1 ou 2");
```

---

# 1.2 Estruturas de repetição (Loop Structures)

## while
```c
while (condicao) {
    // código
}
```

## do-while
```c
do {
    // código
} while (condicao);
```

## for
```c
for (int i = 0; i < n; i++) {
    printf("%d\n", i);
}
```

## Laços aninhados
```c
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        printf("%d %d\n", i, j);
    }
}
```

## Controle
- `break` interrompe o loop
- `continue` pula para próxima iteração

## Complexidade
- O(n)
- O(n²) (aninhado)

---

# 1.3 Modularização (Modularization)

## Funções
```c
int soma(int a, int b); // protótipo

int soma(int a, int b) {
    return a + b;
}
```

## Passagem de parâmetros
Por valor:
```c
void f(int x) { x = 10; }
```

Por referência:
```c
void f(int *x) { *x = 10; }
```

## Escopo
- Local
- Global
- Estático

## Organização
- `.h` → declarações  
- `.c` → implementação  

---

# 1.4 Vetores e Matrizes

## Vetores
```c
int v[10];
```

### Busca linear
```c
int busca(int v[], int n, int x) {
    for (int i = 0; i < n; i++)
        if (v[i] == x) return i;
    return -1;
}
```

## Matrizes
```c
int m[3][3];
```

### Multiplicação
```c
for (i)
 for (j)
  for (k)
    m[i][j] += a[i][k] * b[k][j];
```

---

# 1.5 Recursividade (Recursion)

## Fatorial
```c
int fatorial(int n) {
    if (n == 0) return 1;
    return n * fatorial(n - 1);
}
```

## Fibonacci
```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```

## Recursão de cauda
```c
int f(int n, int acc) {
    if (n == 0) return acc;
    return f(n-1, acc*n);
}
```

---

# COMO ISSO CAI NA PROVA

Você precisa ser capaz de:
- Definir estruturas
- Comparar if vs switch
- Analisar complexidade
- Escrever código em C
- Explicar execução
- Identificar erros (dangling else, stack overflow)

---

# CONCLUSÃO

Este bloco é base da prova.

Domínio esperado:
- Sintaxe em C
- Raciocínio algorítmico
- Clareza teórica
- Escrita técnica
