Controle de fluxo

Nos exemplos vistos até agora o Python executava as ordens sempre na mesma seqüência. E se você quiser alterar esta ordem de execução? Por exemplo, se você quiser que o programa tome algumas decisões e faça coisas diferentes dependendo da situação como imprimir 'Bom dia' ou 'Boa noite' de acordo com a hora do dia?

Como você deve estar pensando, isto é resolvido utilizando-se instruções de controle de fluxo. Existem três instruções de controle de fluxo em Python: if, for e while.

if

A instrução if é usada pra checar uma condição. Se ela for verdadeira alguns comandos serão executados, se ela for falsa outros comandos serão executados. Podemos entender como o comando if funciona se entendermos o seguinte raciocínio lógico:

SE condição:
  comandos1
SENÃO:
  comandos2

Se a condição for verdadeira (retornar True, que equivale a 1, ou um valor positivo) comandos1 serão executados, senão comandos2 serão executados.

A sintaxe correta para o comando if é:

if condição:
  comandos1
else:
  comandos2

Também pode acontecer que seu programa exija uma cadeia de decisões tipo:

SE condição1:
  comandos1
OU SE condição2:
  comandos2
OU SE condição3:
  comandos3
SENÃO:
  comandos4

Se a condição1 for verdadeira, comandos1 serão executados; se condição2 for verdadeira, comandos2 serão executados; se condição3 for verdadeira, comandos3 serão executados e; se nenhuma condição for verdadeira comandos4 serão executados.

A sintaxe correta para este raciocínio é:

if condição1:
  comandos1
elif condição2:
  comandos2
elif condição3:
  comandos3
else:
  comandos4

Abaixo temos um exemplo do uso de if.

Usando o comando if

#! /usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando o comando if

x = int(raw_input("Entre com um número inteiro: "))
if x < 0:
  print 'Número negativo'
elif x == 0:
  print 'Zero'
elif x == 1:
  print 'Um'
else:
  print 'Número positivo'

print 'aqui o programa saiu do if'


Execução do programa:

samuel@aranha:~/python/scripts$ ./if.py
Entre com um número inteiro: -5
Número negativo
aqui o programa saiu do if
samuel@aranha:~/python/scripts$ ./if.py
Entre com um número inteiro: 0
Zero
aqui o programa saiu do if
samuel@aranha:~/python/scripts$ ./if.py
Entre com um número inteiro: 1
Um
aqui o programa saiu do if
samuel@aranha:~/python/scripts$ ./if.py
Entre com um número inteiro: 7
Número positivo
aqui o programa saiu do if
samuel@aranha:~/python/scripts$


Analisando o código:

Na linha:

x = int(raw_input("Entre com um número inteiro: "))

Temos uma novidade, a utilização de funções. Funções serão estudadas mais a frente. Aqui utilizamos duas funções: raw_input( ) e int( ). raw_input( ) exibe uma mensagem na tela e aguarda uma entrada de dados do usuário. Os dados recebidos por ela são entendidos pelo Python como string. Como nosso programa trabalha com números inteiros utilizamos a função int( ) para converter a entrada em inteiros.

Depois temos nosso bloco de intruções if-elif-else que analisa o número digitado e verifica se o mesmo é negativo, zero, um ou positivo. Observe que após cada comando if, elif e else temos dois pontos:

if x < 0:
.....
elif x == 0:
.....
elif x == 1:
.....
else:

este dois pontos são necessários pois definem o bloco de intruções para cada comando if, elif ou else. Observe também que cada bloco de comandos deve possuir a mesma indentação, como já foi explanado em capítulos anteriores.

Após a execução dos comandos if, o programa executa a próxima instrução que apenas exibe uma mensagem com print.

While

A instrução while permite executar um bloco de comandos repetidamente enquanto uma condição for verdadeira. A utilização de while é um exemplo do que é conhecido como looping.

O raciocínio lógico do comando while é:

ENQUANTO condição:
  comando 1
  comando 2
  .....
  comando n


Enquanto a condição for verdadeira os comandos do bloco serão executados. Quando a condição for falsa o próximo comando fora do bloco será executado.

A sintaxe correta de while é:

while condição:
  comandos

Exemplo:

Usando o comando while

#! /usr/bin/python
# -*- coding: iso-8859-1 -*-

print "Utilizando while"
ok = True
while ok:
  caracter = raw_input("Digite qualquer caracter e zero para sair :")
  if caracter == '0':
    ok = False
print 'Encerrando........


Execução:

samuel@aranha:~/python/scripts$ python while.py
Utilizando while
Digite qualquer caracter e zero para sair :a
Digite qualquer caracter e zero para sair :q
Digite qualquer caracter e zero para sair :2
Digite qualquer caracter e zero para sair :3
Digite qualquer caracter e zero para sair :@
Digite qualquer caracter e zero para sair :7
Digite qualquer caracter e zero para sair :0
Encerrando........
samuel@aranha:~/python/scripts$


Analise do código:
Primeiro utilizamos a já conhecida instrução print para exibir uma mensagem. Depois configuramos uma variável chamada ok para o valor True. True e False são tipos boleanos e você pode considerá-los como equivalentes aos valores 1 e 0 respectivamente. Normalmente são usados em situações onde há necessidade de testar se uma condição é verdadeira ou falsa. É uma boa prática usar True e False em vez de valores númericos como zero e um. Observe os dois pontos depois do comando while identificando o início de um bloco de comandos. No bloco de comandos é solicitada uma entrada de dados do usuário e, se o caractere digitado for igual a zero, ok é configurado para False. O bloco de comandos é executado enquanto o caractere digitado for diferente de zero, pois enquanto isto ocorrer ok terá o valor True. Quando zero for digitado o programa encerrará o laço while e a próxima instrução após o laço será executada, no caso o último comando print.

for

A instrução for.....in é outra instrução de looping que itera sob uma seqüência de objetos, isto é percorre cada objeto de uma seqüência. Nós veremos mais sobre seqüências no futuro. Agora você só precisa saber que uma seqüência é uma coleção de itens ordenados.

Exemplo:

Usando o comando for

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

print 'usando o for'
for n in range(1,11):
  print n


Execução:

samuel@aranha:~/python/scripts$ python for.py
usando o for
1
2
3
4
5
6
7
8
9
10
samuel@aranha:~/python/scripts$


Neste programa nós imprimimos uma seqüência de números. A seqüência de números foi gerada utilizando a função interna range( ). Nós fornecemos dois números e range( ) retorna uma seqüência que inicia com o primeiro número e vai até o segundo número exclusive, ou seja, o segundo número não entra na seqüência. No caso range(1,11) retorna a seqüência de 1 até 10. O incremento usado por padrão pela função range( ) é um, porém isto pode ser alterado, basta inserir um terceiro número como argumento. Por exemplo range(1,11,3) retorna [1, 4, 7, 10].

O laço for então itera sobre a seqüencia. for n in range(1,11) equivale a for n in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] que funciona como se atribuíssemos cada número (ou objeto) da seqüencia a n, um de cada vez, e então executássemos o bloco de comandos para cada valor de n. Neste caso nós apenas imprimimos o valor.

Lembre-se que o laço for.....in trabalha com qualquer seqüencia. Aqui nós usamos uma lista de números gerada pela função interna range( ), mas podemos usar qualquer tipo de seqüencia que tenha qualquer tipo de objeto. Exploraremos esta idéia em detalhes mais a frente.

break

A instrução break é usada para quebrar um laço, isto é, parar a execução do looping mesmo que a condição ainda seja verdadeira ou a seqüencia de itens ainda não tenha sido toda iterada.

Exemplo:

Usando o comando break

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

print 'usando o break'

while True:
  s= raw_input('Digite alguma palavra ou SAIR para encerrar :')
  if s == 'SAIR':
    break
  print 'Você digitou uma string de tamanho', len(s)
print 'Encerrando.....'


Execução:

samuel@aranha:~/python/scripts$ python break.py
usando o break
Digite alguma palavra ou SAIR para encerrar :samuel
Você digitou uma string de tamanho 6
Digite alguma palavra ou SAIR para encerrar :total
Você digitou uma string de tamanho 5
Digite alguma palavra ou SAIR para encerrar :sair
Você digitou uma string de tamanho 4
Digite alguma palavra ou SAIR para encerrar :SAIR
Encerrando.....
samuel@aranha:~/python/scripts$


A instrução while True: define uma laço infinito (mais uma vez não esqueça dos dois pontos). Este laço iria ser executado indefinidamente se não fosse por nossa instrução break. No bloco de instruções do laço nós solicitamos uma entrada do usuário, se ele entrar com a string SAIR, chamados break e o laço é encerrado, senão utilizamos a função interna len( ) para retornar o tamanho da string. Observe também que desta vez utilizamos print com dois argumentos separado por vírgula. Ao separar os argumentos de print com vírgula nós suprimimos o caractere de nova linha ao final, o que faz com que os argumentos sejam exibidos lado a lado. Neste caso print insere um espaço entre cada argumento:

>>> print 'usando','print com',2,'vírgulas'
usando print com 2 vírgulas
>>>

A instrução break também pode ser usada com o laço for.

continue

A instrução continue faz a execução pular para a próxima iteração no laço desprezando os comandos posteriores. Exemplo:

Usando o comando continue

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

print 'Usando o continue'

while True:
  s = raw_input('Digite alguma palavra com mais de três letras ou SAIR para encerrar :')
  if s == 'SAIR':
    break
  if len(s) > 3:
    print 'Você digitou uma string de tamanho maior que 3'
    continue
  # se len(s) > 3, “continue” fará com que a instrução abaixo
  # seja desprezada e o programa pulará para a próxima iteração 
  print 'Você digitou uma string de tamanho menor que 3'
print 'Encerrando.....'


Execução:

samuel@aranha:~/python/scripts$ python continue.py
Usando o continue
Digite alguma palavra com mais de três letras ou SAIR para encerrar :teste
Você digitou uma string de tamanho maior que 3
Digite alguma palavra com mais de três letras ou SAIR para encerrar :sim
Você digitou uma string de tamanho menor que 3
Digite alguma palavra com mais de três letras ou SAIR para encerrar :SAIR
Encerrando.....
samuel@aranha:~/python/scripts$


Observe que se o tamanho da string digitada for maior que 3, será exibida uma mensagem e o comando continue desprezará os próximos comandos (no caso um print) e pulará para a próxima iteração. Veja também que se o tamanho da string digitada for menor que 3 os comandos abaixo do continue são executados normalmente.

Outro exemplo do uso do continue

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando continue

for nr in range(1,11):
  if nr % 2 == 0:
    print nr,'é par'
    continue
  print nr,'é ímpar'


Execução:

samuel@aranha:~/python/scripts$ python continue2.py
1 é impar
2 é par
3 é ímpar
4 é par
5 é ímpar
6 é par
7 é ímpar
8 é par
9 é ímpar
10 é par
samuel@aranha:~/python/scripts$


Se o resto de nr dividido por 2 for zero, será exibida a mensagem que o número é par e continue fará o programa pular a próxima instrução continuando a iteração.