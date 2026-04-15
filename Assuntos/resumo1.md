### Resumo da linguagem C até agora

*breve*

## Exercícios

1. Faça uma função que calcula "x elevado na n-ésima potência". A função recebe um `double` e um `int` e retorna um `double`. Pode ser feito de forma iterativa (um produtório). Cuidado com "n" 0 ou negativo. Pode também ser feito de forma recursiva:
   - x elevado a 0 é 1
   - x elevado a n negativo é 1 dividido por x elevado a -n
   - x elevado a n positivo é x multiplicado por x elevado a n-1
2. Faça uma função para calcular o fatorial de x. Use `long` para o tipo do parâmetro e para o valor de retorno. Pode ser feito de forma iterativa (um produtório). Pode também ser feito de forma recursiva:
   - fatorial de número negativo não existe
   - fatorial de 0 é 1
   - fatorial de n positovo é n multiplicado pelo fatorial de n-1
3. Faça uma função para calcular o seno de um ângulo em radianos. Use a série de Taylor:
   ```
   seno(x) = x - x³/3! + x⁵/5! - x⁷/7! ...
   ```
   Interrompa a soma quando tiver somado um termo cujo valor absoluto seja inferior a 10¯¹⁰.
   Use as funções dos exercícios anteriores para o cálculo das potências e fatoriais.
4. Faça um programa que imprime a tabela dos senos de ângulos entre 0 e 89 graus.
   Cada linha deve conter o ângulo (múltiplo de 5) e o seno do ângulo seguido pelo seno dos 4 ângulos subsequentes.
   Imprima os senos com 6 casas decimais.
   Os valores devem estar alinhados na vertical.
5. Faça uma função para o cálculo da raiz quadrada de seu parâmetro. Use o tipo `double` para o parâmetro e o retorno. 
   Use o método de Heron para o cálculo da raiz de *x*:
   - inicie com um chute qualquer (um valor positivo) (*c*)
   - o chute seguinte será a média entre *c* e *x/c*
   - continue até que o erro (pode ser a diferença entre 2 chutes sucessivos) seja inferior a 10¯¹⁰.
6. Faça uma função para calcular o cosseno de um ângulo em radianos. Use as funções acima e a fórmula *sen²x + cos²x = 1*.
1. Refaça a tabela, incluindo o cosseno, e imprimindo com 4 casas depois da vírgula. Fica mais ou menos assim:
   ```
   ang seno   coseno   seno   coseno   seno   coseno   seno   coseno   seno    coseno
    0  0.0000 1.0000   0.0010 0.9090   0.xxxx 0.xxxx   0.xxxx 0.xxxx   0.xxxx 0.xxxx
    5  ...
   10  ...
   ```
   Pontos extras se imprimir em um quadro, com os caracteres unicode de desenho de linhas (por exemplo em https://en.wikipedia.org/wiki/Box-drawing_characters). Para imprimir esses caracteres, pode ser com \u e o código ou copiar da página e colar no printf:
   ```
   printf("└─┤");
   printf("\u2514\u2500\u2524");
   ```
