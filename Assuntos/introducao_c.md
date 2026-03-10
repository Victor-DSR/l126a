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
