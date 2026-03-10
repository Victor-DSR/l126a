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
