## Introdução à linguagem de programação C

Uma linguagem de programação de alto nível permite escrever programas de forma mais abstrata e simples que em linguagem de máquina ou de montagem.
Para que possa ser executado pelo computador, esse programa deve ser traduzido para um programa equivalente em linguagem de máquina.
Um programa em uma linguagem de programação é um texto, que deve ser colocado em um arquivo para que essa tradução seja feita, por um programa chamado "compilador".
O programa traduzido para linguagem de máquina também é colocado em um arquivo (não o mesmo), para que possa ser carregado para a memória pelo sistema operacional para então ser executado pelo processador.

Para que a tradução não seja complicada demais, uma linguagem de programação geralmente é bastante restritiva sobre como o programa deve ser escrito e formatado. A linguagem que vamos usar, chamada "C" não é exceção.

Um programa na linguagem C é dividido em subprogramas chamados **funções**.
Os comandos que representam ações a serem executadas pelo processador necessariamente devem estar em alguma função. A execução de um programa C é entendida como a execução dos comandos de uma função.

Cada função de um programa é identificada por seu nome.
Um programa C pode ter quantas funções quiser, cada uma com um nome diferente.

Uma das funções é especial, e deve ter o nome `main`. 
Essa é a função principal do programa, e são os comandos dessa função que serão executados quando o programa for executado.
As outras funções só serão executadas se um comando, ao ser executado, requisitar a sua execução.
Por enquanto, faremos programas só com uma função (que obrigatoriamente deverá ser chamada `main`).

Uma função é constituída de 4 partes:
- **tipo** (vamos ver mais tarde para que serve, por enquanto basta sabermos que para a função `main` o tipo tem que ser `int`);
- **nome** (pode ser uma sequência qualquer (quase) de caracteres, mas por enquando vai ser `main`)
- **argumentos**, entre parênteses (por enquanto não vamos usar argumentos, mas os parênteses são obrigatórios)
- **corpo**, entre chaves, é aqui que vão os comandos.

Um programa pode não ter nenhum comando. Portanto, o menor programa C possível é um texto com:
```c
int main(){}
```
que instrui o computador para não fazer nada. Não é exatamente um programa útil...

Útil ou não, para poder ser executado, o programa em C deve ser traduzido para código de máquina. O programa em código de máquina deve então ser colocado em um local apripriado da memória, e o processador deve ser instruído a executar a partir desse local.

Temos então 3 tarefas distintas a realizar para executar um novo programa em C:
- produzir um texto com o programa em C. Isso é feito com o auxílio de um programa, chamado editor de textos. Na aula, usamos o editor de textos `nano`, executado com a seguinte linha de comando no linux:
    ```
    nano nome.c
    ```
    onde `nome` é um nome qualquer, que vai ser usado para identificar o programa. Não use espaços no nome. `nano` e `.c` devem estar em minúsculas.
    
    No nano, o programa é gravado com o comando `ctrl-X` (segure a tecla `ctrl` e aperte a tecla `X`).
- compilar esse texto e produzir um arquivo com o programa executável equivalente. Isso é feito por um programa chamado compilador. Em aula, usamos o programa `gcc`, executado com a seguinte linha de comando no linux:
    ```
    gcc nome.c -o nome
    ```
    onde `nome` é o mesmo nome de antes. Esse comando está instruindo o gcc a compilar o programa em C que está no arquivo `nome.c` (chamado programa fonte) e colocar o resultado da compilação no arquivo `nome` (chamado programa executável).

    Durante a execução, o compilador pode emitir mensagens de erro, caso o arquivo não contenha um programa 100% correto de acordo com as regras da linguagem. Nesse caso, o programa deve ser alterado e compilado novamente.
- carregar o programa executável em memória e executá-lo. Isso é feito pelo sistema operacional, com uma linha de comando como abaixo:
    ```
    ./nome
    ```

A linguagem C é uma linguagem bastante simples, e com poucos recursos disponíveis diretamente na linguagem.
Essa simplicidade é compensada com bibliotecas de funções bastante amplas, que contém subprogramas já compilados prontos para serem usados por novos programas. Diretamente na linguagem, não existem nem comandos para realizar entrada ou saída de dados.
Para informar o compilador que nossa programa vai usar alguma dessas funções externas, devemos colocar no início do programa linhas pedindo para incluir alguma biblioteca.
Para entrada e saída, a biblioteca de funções padrão se chama `stdio`. O comando para incluí-la é
   ```c
   #include <stdio.h>
   ```
Após essa inclusão, o programa tem a sua disposição várias funções para realizar entrada e saída de dados. Uma dessas funções chama-se `putchar`, que envia um valor (um `char`) para o dispositivo de saída corrente do programa (que geralmente é o terminal de vídeo).

Para causar a execução de uma função em C, temos o comando de chamada de função. Ele é constituído pelo nome da função seguido de parênteses contendo os parâmetros da função (se ela for parametrizada) seguido pelo caractere `;`.

Juntando tudo isso, podemos fazer um programa que envia o valor `50` para a saída assim:
```c
   #include <stdio.h>

   int main()
   {
       putchar(50);
   }
```

Compilando e executando esse programa, ele irá imprimir `2`.
Isso acontece porque um terminal de vídeo, ao receber um número, interpreta esse número como o código de um comando.
A maior parte desses códigos significa colocar na tela um caractere. O caractere escolhido depende do código. Na quase totalidade dos computadores atuais, essa codificação segue a tabela ASCII, na qual o código 50 corresponde ao caractere `2`.
Caso tenha curiosidade, pode ver esses códigos por exemplo na [wikipédia](https://pt.wikipedia.org/wiki/ASCII).
Dos 128 códigos definidos no padrão ASCII, 95 representam caracteres e os demais representam controles ao terminal. A maior parte dos códigos de controle já não são mais usados. Os mais comuns que são usados representam algumas teclas de controle de um teclado (del, bs, enter, tab) e alguns comandos simples ao terminal (recuar uma posição, recuar para o início da linha, avançar para a linha seguinte). Comandos mais complexos ao terminal (como posicionar o cursor ou trocar a cor dos símbolos) são realizados por sequências do códigos, geralmente iniciadas pelo código ESC.

Para que não necessitemos lembrar dos códigos da tabela, a linguagem permite representar esses valores de outra forma, com o símbolo que se quer entre aspas simples. Por exemplo, `'2'` representa o mesmo valor que `50`. O programa acima é equivalente ao abaixo:
```c
   #include <stdio.h>

   int main()
   {
       putchar('2');
   }
```
Alguns caracteres não são representáveis diretamente dessa forma, notamente os caracteres de controle. Esses valores são representados por 2 caracteres entre as aspas simples, o primeiro deles sempre `\`:
```c
   \n   avanço de linha
   \b   recuo de uma posição
   \a   alarme
   \r   recuo ao início da linha
   \\   \
   \'   '
   \"   "
```
O programa acima pode ser alterado para imprimir o `2` em uma linha inteira:
```c
   #include <stdio.h>

   int main()
   {
       putchar('2');
       putchar('\n');
   }
```

Além de usar funções predefinidas como `putchar`, podemos definir nossas próprias funções, além da `main`.
Todas as funções têm o mesmo formato: `tipo nome (parâmetros) {corpo}`.
No caso da `main`, o tipo obrigatoriamente é `int`, o que quer dizer que a função calcula um valor inteiro.
Esse valor diz ao sistema operacional se houve um erro na execução do programa ou não.
A função main também é uma excessão em que se pode dizer que ela calcula um valor quando ela não calcula nada (que é o caso da nossa função main acima) — nesse caso o compilador deve gerar automaticamente o cálculo de um valor para informar o sistema que não houve erro.
Para as demais funções, é considerado um erro dizer que a função calcula um valor e ela não calcular.
Para dizer que uma função não calcula nada, usa-se o tipo `void`.
Então, se quisermos fazer uma função que só imprime uma linha com `2`, e depois chamarmos essa função na main:

```c
   #include <stdio.h>

   void linha2()
   {
       putchar('2');
       putchar('\n');
   }

   int main()
   {
       linha2();
   }
```

#### Exercício

Complete o programa abaixo, substituindo as partes com `...`, para que ele imprima o seu primeiro nome e último sobrenome.
Não pode alterar o que tá fora do `...`, e só pode usar `putchar`.
Deve ter um espaço separando o nome do sobrenome, e um final de linha após o sobrenome.
```c
   #include <stdio.h>

   void nome()
   {
       ...
   }

   void sobrenome()
   {
       ...
   }

   int main()
   {
       nome();
       sobrenome();
   }
```


Uma função pode receber parâmetros. Quando uma função que recebe parâmetros é chamada, o valor desses parâmetros é colocado dentro dos parênteses no comando de chamada da função, como fizemos nas chamadas a `putchar` acima.
Para criar uma função que recebe parâmetros, coloca-se dentro dos parênteses da função que está sendo criada um nome, que será usado dentro da função toda vez que quisermos referenciar o valor desse parâmetro. Deve-se preceder esse nome de um tipo, que por enquanto usaremos `int` para representar valores que são números inteiros.

Por exemplo, se quisermos uma função que recebe um número como parâmetro e imprime o caractere correspondente entre colchetes, ppodemos fazer assim:

```c
   #include <stdio.h>

   void colch(int c)
   {
       putchar('[');
       putchar(c);
       putchar(']');
   }

   int main()
   {
       colch('X');
       colch('9');
   }
```

#### Exercício

Faça as seguintes alterações no programa que imprime teu nome:
- remova a parte do sobrenome — a função main só chama a função nome
- faça uma função que imprime `+---+` em uma linha
- faça uma função que recebe um número como argumento e imprime uma linha com o caractere codificado por esse número entre `|` e espaços
- altere a função que imprime o nome para usar essa última função para imprimir cada letra, em vez de usar putchar diretamente
- altere a função que imprime o nome para chamar a primeira função descrita, no início e no final do nome

Ao final dessas alterações, o programa deve imprimir como abaixo (para alguém que se chama Juca).
```
   +---+
   | J |
   | u |
   | c |
   | a |
   +---+
```
