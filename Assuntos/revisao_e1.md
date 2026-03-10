O primeiro exercício era:

   Faça um programa que lê 3 valores do teclado e imprime a média deles.
   O programa deve ser escrito em linguagem de montagem e traduzido para linguagem de máquina.

É muito semelhante ao programa para ler e calcular a média de 2 números visto anteriormente.
Precisamos ler 3 números. Cada um é obtido por uma instrução de leitura do dispositivo TECL, que o coloca em uma posição diferente de memória. Chamaremos essas posições de A, B e C. Em linguagem de montagem:
```
     LE TECL, A
     LE TECL, B
     LE TECL, C
```
Agora necessitamos somar os 3 valores obtidos. Só temos instrução para somar 2 valores. Faremos a soma em 2 etapar, primeiro somando A com B e depois somando esse resultado parcial com C. Os resultados da soma devem ser colocados na memória em algum lugar. Chamaremos esses locais de PARCIAL e TOTAL:
```
     SOMA A, B, PARCIAL
     SOMA PARCIAL, C, TOTAL
```
Agora podemos calcular a média, dividindo o total obtido por 3. A instrução de divisão só opera sobre endereços de memória, onde ela busca os valores que usa. Precisamos de um endereço cujo conteúdo seja 3, para fornecer para a instrução. Nosso montador nos permite escrever "#3" e resolve esse problema para nós. Precisamos também de um local onde colocar a média:
```
     DIV TOTAL, #3, MEDIA
```
Já temos a média calculada. Vamos enviá-la para o vídeo e terminar o programa:
```
     ESCR MEDIA, VIDEO
     PARA
```

Traduzindo para linguagem de máquina, sem traduzir os nomes que inventamos:
```
     montagem                  endereços    máquina (sem traduzir nomes)
     LE TECL, A                 0  1  2     2 2 A
     LE TECL, B                 3  4  5     2 2 B
     LE TECL, C                 6  7  8     2 2 C
     SOMA A, B, PARCIAL         9 10 11 12  3 A B PARCIAL
     SOMA PARCIAL, C, TOTAL    13 14 15 16  3 PARCIAL C TOTAL
     DIV TOTAL, #3, MEDIA      17 18 19 20  5 TOTAL #3 MEDIA
     ESCR MEDIA, VIDEO         21 22 23     1 MEDIA 3
     PARA                      24           9
```
O programa ocupa as posições entre 0 e 24, o restante da memória está disponível para colocarmos os dados que usamos. Vamos colocá-los em ordem, iniciando pelos que devem ter valor associado (para ficar mais fácil de fazer o mapa de memória):
```
     endereço   nome
     25         #3
     26         A
     27         B
     28         C
     29         PARCIAL
     30         TOTAL
     31         MEDIA
```
O programa completo em linguagem de máquina fica então:
```

```
```
    endereços    máquina
     0  1  2     2 2 26
     3  4  5     2 2 27
     6  7  8     2 2 28
     9 10 11 12  3 26 27 29
    13 14 15 16  3 29 28 30
    17 18 19 20  5 30 25 31
    21 22 23     1 31 3
    24           9
    25           3
```

No segundo exercício, pedia-se para converter o conteúdo da memória no programa em linguagem de montagem correspondente, para 4 mapas de memória apresentados. Além disso, deduzir o que cada programa faz.

O programa 1 era o mesmo programa visto antes, para o cálculo da média de dois números.
O programa 2 está abaixo:

.            | .   | .   | .   | .   | .   | .   | .   | .   | .   | .
-----------: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: 
**endereço** |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9
**valor**    | 2 | 2 | 18 | 2 | 2 | 19 | 8 | 18 | 19 | 14 
||||||||||
**endereço** | 10  | 11  | 12  | 13  | 14  | 15  | 16  | 17  | 18  | 19
**valor**    |  4 | 19 | 20 | 18 | 1 | 18 | 3 | 9 | 0 | 0 |
||||||||||
**endereço** | 20 
**valor**    |  0 

A primeira instrução está no endereço 0.
Nesse endereço tem o valor 2, que corresponde à instrução "LE".
Essa instrução é codificada em 3 endereços, no caso 0, 1 e 2.
Nesses endereços estão os valores 2, 2 e 18.
Os argumentos da instrução LE são o número do dispositivo (2 representa o teclado) e o endereço onde o valor lido vai ser colocado (no caso, 18).
Em linguagem de montagem, indicando o endereço da instrução e ainda sem dar nome ao endereço que é argumento:
```
0: LE TECL, 18
```
Usando a mesma ideia para as demais instruções:
```
 0: LE TECL, 18
 3: LE TECL, 19
 6: DESVM 18, 19, 14
10: SUB 19, 20, 18
14: ESCR 18, VIDEO
17: PARA
```
Para dar nomes aos endereços, identificamos:
- endereços que correspondem a instruções (aqueles que são destino de desvios)
- endereços que só são lidos pelas instruções (representam valores constantes)
- endereços que são destino de instruções que escrevem na memória (normalmente representam valores que são manipulados pelo programa e podem receber nomes que representam seu uso)

No primeiro caso, temos o endereço 14, vamos chamá-lo de "LOGOALI".
No segundo caso, temos 20, o valor em 20 é 0, vamos designá-lo por "#0".
No terceiro caso, temos 18 e 19, vamos chamá-los de V1 e V2.
Alterando no programa:
```
         LE TECL, V1
         LE TECL, V2
         DESVM V1, V2, LOGOALI
         SUB V2, #0, V1
LOGOALI: ESCR V1, VIDEO
         PARA
```
Esse programa lê dois valores, depois compara eles e, se o primeiro for maior que o segundo, pula a instrução SUB. A instrução SUB, que só será executada so o primeiro valor não for maior que o segundo, subtrai 0 de V2 e coloca o resultado em V1 (isso equivale a fazer com que V1 passe a ter o valor de V2). Depois, ele imprime o valor de V1.
O programa vai imprimir o primeiro valor se ele for maior que o segundo, senão ele vai imprimir o segundo. Em outras palavras, ele imprime o maior entre os dois valores digitados.

