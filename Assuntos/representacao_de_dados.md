## Representação de dados

A forma usada pelos computadores para representar números internamente é semelhante à forma mais usual que usamos para isso: uma sequência de dígitos que representam valores, cada um com um peso diferente conforme a posição.

Quando escrevemos "123", o dígito "1" tem o valor cem porque está na terceira posição, o dígito "2" tem o valor vinte porque está na segunda posição, e o dígito "3" tem o valor três porque está na primeira posição.
Cada posição tem um peso que é uma potência de 10.
O valor total representado por "123" é cento e vinte e três: 1×10² + 2×10¹ + 3×10⁰.

A memória do computador é implementada como uma enorme quantidade de dígitos.
Enorme, mas finita.
Temos que definir a quantidade de dígitos a usar para um número, mas tem alguns conflitos a resolver:
- se escolhemos poucos dígitos, a gama de valores possível é limitada;
- se escolhemos muitos dígitos, usaremos mais memória e consequentemente reduziremos a quantidade de números que poderemos manipular simultaneamente (e no computador, tudo são números);
- se escolhemos muitos dígitos, o tempo necessário para cada operação será maior.

Os fabricantes de computadores e de linguagens de programação implementaram uma certa flexibilidade, e cabe ao programador escolher o número de dígitos que será usado por cada número manipulado por seu programa.
Cada número tem um **tipo**, que define quantos dígitos serão usados por esse número e de que forma esses dígitos serão interpretados.

Uma forma de interpretação dos dígitos é a usada para representar números inteiros, outra é a usada para representar números reais (chamados de ponto ou vírgula flutuante).
No caso de números inteiros, a quantidade de dígitos utilizada vai definir o maior valor representável.
Operações que produzam resultados maiores que esse limite não podem ter esse valor representado corretamente, resultando em um erro.
Por exemplo, se os números forem representados com 3 dígitos, o resultado da operação "123+923" não seria representável nesse mesmo formato; qualquer dos 1000 valores representáveis corresponderia a um resultado errado.

No caso de números de ponto flutuante, se usa em computadores uma notação semelhante à notação científica: o número 1.23 poderia ser escrito como "123×10¯²", e representável como 2 números inteiros: a potência de 10 (chamado expoente, no caso -2) e os dígitos significativos (chamado mantissa, no caso 123).
Como é necessário definir a quantidade de dígitos usados para um número, nesse caso tem que definir duas quantidades: o número de dígitos para o expoente e o número de dígitos para a mantissa.
Definindo uma quantidade fixa para cada um deles, tem-se algumas consequências na gama de valores que se consegue representar.

Para exemplificar essas limitações, vamos considerar um caso extremo, em que usamos um dígito para o expoente e um dígito para a mantissa.
Com o expoente sempre positivo, a posição do ponto decimal quando o expoente for 0 será 4 casas antes do dígito da mantissa. A representação 01 codifica 0 para o expoente e 1 para a mantissa e representa o valor 0.00001.
O menor valor representável é 00, que representa 0; o segundo menor valor é 01, que representa 0.00001; o terceiro menor valor é 0.00002.
O maior valor representável é 99, que representa 90000; o segundo maior valor é 98, que representa 80000.
Se consegue representar todos os valores que têm um só dígito diferente de 0, entre 10¯⁵ e 10⁴.

Se esse mesmos dois dígitos fossem usados para representar um valor inteiro, se conseguiria representar todos os valores inteiros entre 0 e 99.
Em inteiro, a gama de valores é menor, mas se consegue representar todos os valores inteiros até o limite. Em ponto flutuante, se consegue representar uma gama bem maior de valores, mas com menor resolução (não se diferencia os valores 10 e 11 na representação acima, por exemplo).

A grande maioria dos computadores atuais (se não todos) representam os números internamente em formato binário, e não decimal.
Os motivos são vários, como:
- é mais fácil e barato de representar um dígito que pode ter só dois valores diferentes do que um que pode ter 10 valores, com as grandezas tipicamente usadas para representá-los (tensão elétrica, carga elétrica, corrente elétrica, magnetização, intensidade luminosa, etc);
- é mais fácil e barato construir um circuito que realize operações aritméticas em binário (compare a tabuada decimal e a tabuada binária, por exemplo).

### Representação de números inteiros naturais (sem sinal)

Em binário, um dígito (chamado de bit) só tem dois valores possíveis (tipicamente representados por "0" e "1").
Cada posição em uma sequência de dígitos representa uma potência de 2 (o dígito mais à direita representa 1, o segundo 2, o terceiro 4 etc). Os dígitos binários "101" representam o valor cinco (1×4 + 0×2 + 1×1).

Com 10 dígitos binários (bits) se tem aproximadamente o mesmo poder de representação que 3 dígitos decimais (se consegue representar 1024 valores diferentes com 10 bits e 1000 com 3 dígitos decimais).

Para se poder representar um valor, se necessita um número mínimo de dígitos, que é maior quanto maior for o valor.
Um determinado computador tem uma determinada capacidade de memória, que é medida em bytes (um byte é um grupo de 8 bits).

Os tipos básicos da linguagem estão abaixo. Existem 6 tipos inteiros sem sinal, 5 tipos inteiros com sinal, 3 tipos ponto flutuante reais e 3 tipos ponto flutuante complexos (com um número para a parte real e outro para a parte imaginária).
Em C existem cinco tipos de dados inteiros padrão, com duas versões cada, com e sem sinal (os tamanhos não são padronizados, abaixo estão os tamanhos habituais em um PC atual):

| nome do tipo | bits | gama de valores representáveis |
| ---: | ---: | :--- |
| bool | 1 | false e true (0 e 1) |
| unsigned char | 8 | 0 a 255 (2⁸-1) |
| unsigned short | 16 | 0 a 65535 (2¹⁶-1) |
| unsigned int | 32 | 0 a 4bi (2³²-1) |
| unsigned long | 64 | 0 a 16 quintilhões (2⁶⁴-1) |
| unsigned long long | 64 | 0 a 16 quintilhões (2⁶⁴-1) |
|   |   | . |
| signed char | 8 | -128 a 127 |
| signed short | 16 | -32768 a 32767 (2¹⁵-1) |
| signed int | 32 | -2bi a 2bi (2³¹-1) |
| signed long | 64 | -8qui a 8 quintilhões (2⁶³-1) |
| signed long long | 64 | -8qui a 8 quintilhões (2⁶³-1) |
|   |   | . |
| float | 32 | 6 dígitos; 10¯³⁸ a 10³⁸ |
| double | 64 | 16 dígitos; 10¯³⁰⁸ a 10³⁰⁸ |
| long double | 128 | não sei |
|   |   | . |
| float complex | 2×32 | 6 dígitos; 10¯³⁸ a 10³⁸ |
| double complex | 2×64 | 16 dígitos; 10¯³⁰⁸ a 10³⁰⁸ |
| long double complex | 2×128 | não sei |


Se um tipo inteiro (exceto `char`) não tiver `signed` nem `unsigned`, é considerado `signed`.
O tipo `bool` foi introduzido na versão C23; em versões mais velhas pode ser necessário incluir `<stdbool.h>` para ter acesso a esse tipo.
A aritmética inteira é feita com os tipos `int` ou maior; os valores menores são promovidos a `signed int` antes de serem operados.


### Exercício

1. Faça um programa que imprime os primeiros 10 valores `int` que não são representáveis como `float`.
Para saber se um número que está em uma variável inteira é representável como float, transfira-o para uma variável do tipo float e depois dessa para uma variável do tipo int. Se o valor na última variável for igual ao da primeira, o valor é representável como float.
2. Faça uma programa para encontrar o maior valor `float` que somado ao valor 1 `float` não altera o 1.
   Dica: use 2 variáveis para conter um valor que é grande (causa alteração) e outro que é muito pequeno (não causa alteração), e chuta um valor no meio. Dependendo se o valor chutado causa ou não alteração, altera um ou outro dos limites. Dá para repetir até o chute ser igual a um dos limites.

* * *

<!-->
Incluindo `<limits.h>`, tem-se acesso a algumas constantes com valores relativos aos tipos de dados inteiros, como `CHAR_WIDTH`, que tem o número de bytes em um `char`, `USHRT_MAX`, que tem o maior valor representável em um `unsigned short`, `INT_MIN`, que tem o menor valor representável em um `int`.
Nessas constantes, os tipos são `CHAR`, `SHRT`, `INT`, `LONG`, `LLONG`, podendo ser precedidos de `U` para `unsigned`. As constantes `_MIN` não existem para os tipos `unsigned` (o valor mínimo nesse caso é sempre 0). 

### Valores literais

Em C, se chama de "literais" os valores constantes. Esses valores também têm um tipo. Eles podem ser escritos de várias formas:
- sequência de dígitos decimais não iniciada por `0`: valor do tipo `int` ou `long` ou `long long`, o menor que consegue representar o valor.
- sequência de dígitos octais iniciada por `0`: valor inteiro em octal. O tipo será `int` se o valor couber, senão, `unsigned int` se couber, senão, `long` ou `unsigned long` ou `long long` ou `unsigned long long`.
- sequência de dígitos hexadecimais iniciada por `0x`: valor inteiro em hexadecimal. O tipo é como para octais.
- sequência de dígitos binários iniciada por `0b`: valor inteiro em binário. O tipo é como para octais.
- 


<!--
## *float*

Até agora, os dados que usamos eram todos inteiros. Eles são suficientes para muitos programas, mas às vezes necessitamos tratar com valores que não são inteiros. A linguagem C tem o tipo de dados `float` para essas situações.
Em computação, é comum chamar valores com vírgula de "ponto flutuante" ou "vírgula flutuante", para ressaltar suas limitações em relação ao conjunto de números reais da matemática. (Talvez devessem fazer a mesma coisa com os inteiros).

Considere o programa abaixo:
```c
#include <stdio.h>

int main()
{
  float a, b, m;
  printf("Digite dois números: ");
  scanf("%f%f", &a, &b);
  m = (a + b) / 2.0;
  printf("A média entre %f e %f é %f.\n", a, b, m);
}
```
Nesse programa:
- variáveis são declaradas como do tipo `float`;
- a leitura de variáveis do tipo `float` com scanf é feita com o formato `%f`;
- a escrita de valores do tipo `float` com printf é feita com o formato `%f`;
- constantes de ponto flutuante são escritas com um `.` (não pode usar `,`).

Algumas considerações:
- os números `float` são implementados internamente como dois inteiros, chamados de mantissa e expoente.
A mantissa contém os dígitos que compõem o número e o expoente contém a posição da vírgula (por isso o nome de "flutuante").
Por exemplo, o número `1,23` poderia ser representado em decimal como `(123, -2)`, com o significado de `123×10⁻²`
- em geral o tipo `float` é implementado com 4 bytes, 3 para a mantissa e um para o expoente. Isso corresponde em decimal a entre 6 e 7 dígitos para a mantissa, com a vírgula podendo ser deslocada aproximadamente 38 casas decimais para a esquerda ou para a direita.
- essas limitações fazem com que se possa armazenar números bastante grandes (até 10³⁸) e bastante pequenos (até 10⁻³⁸), mas não se consegue distinguir entre 98765435 e 98765429, por exemplo.
- quando imprime números `float` com `%f` no `printf`, ele imprime sempre com 6 dígitos depois da vírgula.
Para mudar, pode-se usar `%.2f`, por exemplo, para pedir para ele imprimir com 2 dígitos depois da vírgula.

### Mais tipos de dados

Outros tipos de dados em C:
- tipos inteiros: `char`, `short`, `int`, `long`, `long long`
- tipos de ponto flutuante: `float`, `double`, `long double`

Quanto mais para a esquerda nessas listas de tipos, menor o espaço ocupado e menor a gama de valores representados.
A linguagem C não especifica o espaço ocupado por cada tipo, só diz que esse tamanho de um tipo não pode ser menor que o tipo à sua esquerda na lista.

No computador que estou usando agora, e com o compilador gcc, esses tamanhos são, em bytes:
| tipo        | tamanho | valores representáveis |
| ---:        |    ---: | :--- |
| `char`        |       1 | -128 a 127 ou 0 a 255 |
| `short`       |       2 | -32768 a 32767 |
| `int`         |       4 | -2 a +2 bilhões |
| `long`        |       8 | -4 a +4 quintilhões |
| `long long`   |       8 | idem |
| `float`       |       4 | ±7 dígitos, ±10³⁸ |
| `double`      |       8 | ±16 dígitos, ±10³⁰⁸ |
| `long double` |      16 | sei lá |

Para ler ou escrever valores desses tipos, devemos usar formatos específicos com `printf` e `scanf` (nem sempre são iguais):
| tipo        | `printf` | `scanf` |
| ---:        |    :--- | :--- |
| `char`        | `%c` ou `%d` | `%c` ou `%hhd` |
| `short`       | `%c` ou `%d` | `%hd` |
| `int`         | `%c` ou `%d` | `%d` |
| `long`        | `%ld`      | `%ld` |
| `long long`   | `%lld`     | `%lld` |
| `float`       | `%f`       | `%f` |
| `double`      | `%f` ou `%lf`| `%lf` |
| `long double` | `%Lf`      | `%Lf` |

Além desses tipos, existe o tipo `bool`, usado para representar valores lógicos.
Só existem dois valores desse tipo, e eles recebem nomes, `true` para representar verdadeiro e `false` para representar falso. Esses valores são transformados para `1` e `0` respectivamente, se forem convertidos para um valor numérico. A conversão contrária, de um valor numérico em `bool`, converte o valor `0` em `false` e qualquer outro valor em `true`.

### Mais detalhes

Nos tipos inteiros, pode-se colocar `signed` ou `unsigned` antes do tipo, para dizer se se quer possibilitar a representação de valores negativos ou não. Um tipo "unsigned" pode representar o dobro dos valores positivos que um tipo "signed" (mas não pode representar valores negativos). Por exemplo, um "signed int" de 4 bytes pode representar valores entre -2 e +2 bilhões, e um "unsigned int" de 4 bytes pode representar valores entre 0 e 4 bilhões.

Quando não se especifica nem "signed" nem "unsigned", é considerado como "signed", exceto para o tipo "char", que não foram capazes de decidir na norma, e depende do compilador.

Para ler um valor unsigned com scanf ou escrever com printf, tem que substituir o formato `d` por `u` (`%lu` para um unsigned long, por exemplo).

Dá para ler ou escrever valores unsigned em outras bases além de decimal, trocando o formato `d` por `o` para octal, `x` para hexadecimal ou `b` para binário.

Valores inteiros constantes no corpo de um programa também podem ser escritos nessas outras bases: se iniciar com `0` e for seguido de dígitos entre `0` e `7`, está em base octal, se iniciar com `0x` está em base hexadecimal e `0b` em binário.
```c
  // todas as atribuições abaixo colocam o valor dez em x
  int x;
  x = 10;
  x = 012;
  x = 0xa;
  x = 0b1010;
  x = '\n';
```

Quando se imprime um número com `%d`, a função printf vai usar o número mínimo de caracteres necessários para imprimir o valor pedido. Se for impresso o valor 52, usará 2 caracteres, se for impresso -128, usará 4.
Caso se queira que o printf use um número mínimo de caracteres, pode-se colocar esse valor entre o `%` e o `d`. Por exemplo, `%3d` irá imprimir o valor 52 com 3 caracteres, colocando um espaço antes do `5`. Dá para escolher `0` em vez de espaço com `%03d`.

Isso funciona também para valores em ponto flutuante. `%10f` vai imprimir pelo menos 10 caracteres: 3 antes do ponto, o ponto e 6 dígitos depois do ponto. `%7.2f` vai imprimir pelo menos 4 antes do ponto, o ponto e dois dígitos depois.
Caso o número seja muito grande ou muito pequeno, o printf usará notação científica, com o caractere `e` sendo usado para significar "vezes 10 elevado na potência". Por exemplo, 123456 pode ser impresso como 1.234560e+05, e 0.0001 pode ser escrito como 1.000000e-04. Essa mesma forma pode ser usada para representar constantes em ponto flutuante no interior de um programa C ou para a entrada de dados, em resposta a um scanf.

### Mais detalhes sobre expressões aritméticas

Em uma expressão aritmética, podemos usar os operadores aritméticos da linguagem para codificar a realização de operações aritméticas entre os valores gerenciados por nosso programa.
A linguagem tem 5 operadores aritméticos, `+-*/%`, que codificam as operações de soma, subtração, multiplicação, divisão e resto da divisão.

Em uma CPU, tem-se várias implementações dessas operações, para os vários tipos e tamanhos de dados que a CPU é capaz de operar. Para cada uma dessas operações, a CPU tem uma instrução distinta. Em geral, uma instrução que opera sobre valores de um tipo produz resultado desse mesmo tipo (a instrução que divide um inteiro de 32 bits por outro inteiro de 32 bits produz como resultado um inteiro de 32 bits).

Em C, usa-se os mesmos símbolos para codificar todas elas. O compilador deve então ter uma maneira de escolher a instrução adequada cada vez que tem que compilar uma expressão aritmética.
A regra da linguagem é a seguinte:
- a expressão é analisada, e a ordem de execução dos operadores é decidida;
- para cada operador, o compilador verifica os tipos de seus operandos;
- se os dois operandos forem do mesmo tipo, a operação será realizada com esse tipo, e o resultado da operação será do mesmo tipo;
- se os dois operandos forem de tipos diferentes, um dos operandos tem seu valor convertido para o tipo do outro - agora os dois têm o mesmo tipo, e a escolha é como acima;
- o tipo escolhido é o que está mais abaixo entre os dois, na tabela de tipos vista acima (entre dois inteiros ou dois de ponto flutuante, é escolhido o de maior tamanho; entre um inteiro e um ponto flutuante, é escolhido o de ponto flutuante).

Por exemplo, considere o código abaixo:
```c
  float r;
  int a = 9;
  r = 3.5 + a / 2 - 2;
```
A ordem das operações será divisão, soma, subtração. Para a divisão, `a` e `2` são inteiros, a divisão será inteira, o resultado é 4. Para a soma, 3.5 é float, 4 é int, a operação e o resultado serão float; 4 inteiro é convertido em 4.0 float, o resultado é 7.5. Para a subtração, 7.5 é float, 2 é int, o resultado será 7.5. Por último vem a atribuição, o valor à direita é float e a variável também, a atribuição é direta. Se `r` fosse int, o valor 7.5 teria que ser convertido para int e seria atribuído o valor 7.

### Exercício

1. O que será impresso pelo programa abaixo? Responda só analisando o código, confira sua resposta executando ele. Se programa não imprimir igual a sua resposta, entenda por que; pode colocar outros printf para conferir os valores intermediários, se ajudar.
```c
#include <stdio.h>

int f(int a)
{
  int x;
  x = 2.5 * a;
  printf("%d ", x);
  return x + 2;
}

int main()
{
  int a, b, x;
  a = 3;
  x = a - 1.5;
  b = x * a;
  printf("%d\n", a);
  a = f(b);
  printf("%d %d\n", a, x);
}
```
2. Faça um programa que lê os coeficientes `a`, `b` e `c` de uma equação de segundo grau (`y = a x² + b x + c`). O programa deve imprimir o número de raízes reais distintas que a equação tem. Os coeficientes são `float`.
3. Altere o programa acima para, após ler o valor dos coeficientes, ler o valor de `x`. O programa deve então chamar uma função para calcular o valor de `y` e imprimir esse valor.
-->
