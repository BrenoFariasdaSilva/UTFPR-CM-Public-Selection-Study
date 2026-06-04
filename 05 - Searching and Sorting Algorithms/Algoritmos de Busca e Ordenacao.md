# Algoritmos de busca e ordenação

## 1. Introdução

Busca e ordenação compõem o núcleo clássico da análise de algoritmos. Quase todo sistema computacional, direta ou indiretamente, depende de localizar registros, manter coleções ordenadas, mesclar conjuntos ou reorganizar dados para acelerar consultas. A história da área é marcada precisamente por avanços nesse domínio, desde métodos quadráticos elementares até estratégias assintoticamente sofisticadas e sensíveis à arquitetura de memória (Knuth, 1998; Cormen et al., 2009).

## 2. Fundamentação Teórica

O problema de busca consiste em determinar a presença e, em geral, a posição de uma chave em uma coleção. O problema de ordenação consiste em permutar os elementos de uma sequência segundo uma relação de ordem. Esses problemas estão intimamente ligados: uma vez ordenados, os dados admitem buscas sublineares como busca binária. Em contrapartida, ordenar pode custar mais do que sucessivas buscas lineares quando o volume de consultas é pequeno.

Estabilidade, adaptatividade, uso de memória extra e comportamento em melhor, médio e pior caso são atributos decisivos. Algoritmos estáveis preservam a ordem relativa de chaves iguais. Algoritmos in-place usam memória adicional assintoticamente constante ou muito pequena. Métodos por comparação obedecem ao limite inferior $\Omega(n \log n)$ no pior caso médio, enquanto abordagens como Counting Sort e Radix Sort exploram propriedades das chaves para superar esse limite em contextos específicos (Cormen et al., 2012).
