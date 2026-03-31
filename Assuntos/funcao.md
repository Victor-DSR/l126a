### Função

Um programa na linguagem C é dividido em subprogramas chamados **funções**.
Os comandos que representam ações a serem executadas pelo processador necessariamente devem estar em alguma função.
A execução de um programa C é entendida como a execução dos comandos de uma função.

Cada função de um programa é identificada por seu nome.
Um programa C pode ter quantas funções quiser, cada uma com um nome diferente.
Para que uma função seja executada, ela deve ser "chamada" por outra.
A chamada de uma função é a execução de um comando que pede que uma função seja executada, enquando a função chamadora aguarda, até que a função chamada encerre sua execução (se diz que a função chamada retorna), quando a função chamadora continua a executar.

Quando uma função é chamada, ocorre a *passagem de parâmetros*, em que valores fornecidos pela função chamadora (chamados *argumentos*) são passados para variáveis especiais da função chamada (chamados *parâmetros*).
Após isso, a função inicia sua execução. Quando a execução da função termina, ocorre o *retorno*, potencialmente transferindo um *valor de retorno* da função chamada para a função chamadora.

Uma função é constituída de 4 partes:
- **tipo** — o tipo do valor retornado pela função; caso a função não retorne valor, o tipo deve ser `void`;
- **nome** — identifica a função; é uma sequência de caracteres, o primeiro obrigatoriamente uma letra, os demais podem ser letras, números ou "_"
- **parâmetros**, entre parênteses, separados por vírgulas. Cada parâmetro é constituído pelo tipo do valor que o parâmetro recebe e por seu nome;
- **corpo**, entre chaves; aqui vão as declarações de variáveis das funções e sentenças a executar quando a função for chamada.

O final da execução de uma função acontece quando ela executa o comando `return`. Se a função for `void`, o comando `return` é somente
```c
   return;
```
Se a função não for `void`, o comando `return` é
```c
   return expressão;
```
Nesse caso, o comando calcula o valor da expressão e esse constitui o valor retornado para a função chamadora.

Uma função `void` pode não executar o comando `return` (ou nem possuir esse comando). Nesse caso, a função termina ao executar o `}` final da função.

A função `main` é a única função que não é `void` que pode terminar sem executar `return`. Nesse caso, considera-se que ela retorna o valor 0.

Por exemplo, a função abaixo recebe dois `int` como parâmetros e retorna o maior deles:
```c
   int maior(int a, int b)
   {
       int m = a;
       if (a < b) m = b;
       return m;
   }
```
Essa função poderia ser chamada com:
```c
   x = maior(y, z);
```
Funciona mais ou menos assim:
Os valores dos argumentos da função são calculados na função chamadora (nesse caso, os valores de y e z).
Esses valores são colocados em uma área de transferência (chamada pilha de execução) e a execução da função chamadora é suspensa.
A função chamada é então ativada -- é alocada memória para seus parâmetros e demais variáveis locais, os valores dos argumentos são passados para os parâmetros e a função chamada inicia sua execução.
A função executa uma sentença por vez a partir de sua primeira sentença até executar o comando `return`, quando ela calcula o valor de retorno, coloca na área de transferência, libera memória das variáveis locais (incluindo parâmetros) e é desativada.
A função chamadora é reativada no ponto onde estava.
A função chamadora então remove o valor de retorno área de transferência e usa ele na expressão que contém a chamada da função (no exemplo, atribuindo esse valor à variável `x`).

Pode-se passar quantos valores se queira para uma função (desde que se declare um parâmetro para cada valor), mas só se pode retornar um valor (ou nenhum, para funções `void`).

O valor de retorno de uma chamada de função pode ser usado em qualquer lugar que necessita um valor:
```c
   x = maior(y, z);
   x = 7 / maior(y, z);
   printf("maior: %d", maior(y, z));
   x = maior(w, 3 * maior(y, z));
```
