## Entrada e saída com printf e scanf

Como já vimos, a função `printf` permite a impressão de caracteres na saída padrão (tela do monitor).
O primeiro parâmetro dessa função é uma *string*, que contém uma sequência de caracteres a enviar para a saída.
Além de caracteres "normais", que são enviados à saída sem alteração, a função trata pedidos de formatação de dados, que iniciam com o caractere `%`.
O uso típico de um pedido de formatação é imprimir uma representação textual de um valor obtido em um parâmetro para `printf`. O primeiro pedido de formatação irá formatar o primeiro parâmetro após a *string*, o segundo pedido formata o segundo parâmetro etc.

Um pedido de formatação inicia por `%` e termina por uma letra que identifica o tipo de formatação que se deseja e o tipo do dado que será formatado.
É obrigação de quem chama `printf` passar argumentos do tipo definido no pedido de formatação.

Os principais pedidos de formatação são `%d`, que imprime um valor do tipo `int` em decimal e `%f`, que imprime um valor do tipo `double` em decimal, com 6 casas depois do ponto.
Por exemplo,
```c
   int i = 240;
   double f = 5.37;
   printf("%d %f", i, f);
```
irá imprimir `240 5.370000`.

O formato da conversão pode ser configurado com caracteres entre o `%` e o `d` ou `f`. Os mais comuns são:
- um número (chamado largura), que diz quantos caracteres no mínimo devem ser usados para imprimir o número. No exemplo acima, se fosse "%5d %10f", seria impresso `  240   5.370000`.
- um número (chamado precisão), precedido de `.`, que diz quantos dígitos no mínimo devem ser impressos no caso de `%d` e quantos dígitos devem ser impressos depois do `.` no caso de `%f`. No exemplo acima, `%.4d %.1f` imprimiria `0240 5.4`.

Os dois podem ser usados juntos: `%5.4d %10.1f` imprimiria ` 0240        5.4`

O pedido `%%` é diferente, ele simplesmente imprime o caractere `%`, e não usa um parâmetro.

O pedido `%d` imprime um `int`, e pode ser usado também para imprimir qualquer tipo inteiro menor que `int`, porque são convertidos para `int` na chamada a uma função cujos argumentos não têm tipo definido (como é o caso de `printf`). Por exemplo,
```c
   char a = 'A';
   printf("%d", a);
```
vai imprimir `65`. O mesmo ocorre para os tipos `short` e `bool`.

O `%i` é um sinônimo para `%d`. `%u`, `%x`, `%X` e `%b` servem para imprimir valores do tipo `unsigned int` em decimal, hexadecimal, hexadecimal com maiúsculas ou binário.

Para imprimir tipos inteiros maiores que int, usa-se um `l` ou `ll` (para `long` ou `long long`) antes da letra. Por exemplo, `%.40llb` para imprimir um `unsigned long long` com pelo menos 40 dígitos binários.

O formato `%c` serve para imprimir um caractere. O argumento do tipo `int` é convertido para `unsigned char` e o valor resultante é enviado para a saída, como o código do caractere a imprimir.

Para números em ponto flutuante, se for enviado um valor do tipo `float` para o `printf`, esse valor será convertido para `double` antes da passagem de argumento, de forma que pode ser impresso com `%f` da mesma forma que valores do tipo `double`. Valores `long double` devem ser impressos com `%Lf`.

Além de `%f`, pode-se imprimir valores de ponto flutuante com
- `%e` ou `%E`, que vai imprimir o número em notação científica (51 impresso com `%.2E` será impresso `5.10E+01`.
- `%g`, que imprime como `%e` se o valor for inferior a 10¯⁴ ou como `%f`, mas não imprimindo caracteres `0` no final da parte fracionária nem `.` se todos os dígitos após o `.` forem `0`.

### Exercícios

1. Faça um programa para imprimir uma tabela com os números de 1 a 10 e seus quadrados. O 1 e seu quadrado na primeira linha, 2 na segunda etc. Os valores devem ficar alinhados verticalmente.
1. Faça uma função para calcular e retornar a raiz quadrada de seu parâmetro. Tanto o parâmetro quanto a raiz devem ser `float`. Para calcular a raiz, use o seguinte método: inicialize duas variáveis, uma com um valor certamente menor que a raiz e outro com um valor certamente maior que a raiz. Faça um laço que chuta que a raiz está no meio do intervalo e altera um dos limites do intervalo se o valor chutado for muito grande ou muito pequeno. Considere que o valor da raiz é o meio do intervalo após 20 repetições do laço.
1. Altere o primeiro programa para incluir a raiz quadrada de cada valor na tabela, também alinhada. Imprima a raiz com 3 casas após a vírgula. Use a função acima para o cálculo da raiz. O programa deve usar uma função para formatar um número (recebe o número como parâmetro e imprime o número, o quadrado e a raiz).
1. Altere o programa anterior para ter os números de 1 a 30, em três colunas: na primeira coluna tem os números de 1 a 10 com seus quadrados e raízes quadradas, na segunda os números de 11 a 20 e na terceira de 21 a 30. Além da função para formatar um número, o programa deve ter uma função para formatar uma linha (recebe o número da primeira coluna como parâmetro, chama a função de formatar um número 3 vezes).
   A primeira linha vai conter os números 1, 11 e 21, a segunda conterá 2, 12e 22 etc.
