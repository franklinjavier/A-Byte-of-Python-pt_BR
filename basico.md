Básico

Números

Os números em Python são de quatro tipos – inteiros, inteiros longos, de ponto flutuante e complexos:

Exemplo de inteiros são 2 e 7;

Inteiros longos são números inteiros bem grandes;

Exemplos de números de ponto flutuante são 3.23 e 52.3E-4. A notação E indica potência de 10. Neste caso, 52.3E-4 significa 52.3 * 10-4;

Exemplos de números complexos são (-5+4j) e (2.3-4.6j)

Strings

Uma string é uma seqüência de caracteres. Você tem três maneiras de usar as strings:

Usando aspas simples ( ' )

Você pode especificar as strings usando aspas simples como em: 'utilizando strings em Python'. Todos espaços em branco e tabulações são preservados.

Usando aspas duplas ( “ )

Strings envolvidas em aspas duplas trabalham da mesma maneira que as envolvidas em aspas simples. Um exemplo seria: ”Strings também podem estar entre aspas duplas”.

Usando aspas triplas ( ''' ou “””)

Você pode especificar strings com mais de uma linha usando aspas triplas. Você pode usar aspas simples ou aspas duplas livremente dentro de strings envolvidas em aspas triplas. Um exemplo seria:

''' Esta é uma string com mais de uma linha. Esta é a primeira linha.
Esta é a segunda linha.
“Qual seu nome ?”, eu perguntei.
Ele disse ”Uel, Ma...nuel.”
'''

Seqüências de escape

Digamos que você quer uma string que contenha uma aspas simples ( ' ), como você especificará esta string ? Por exemplo What's your name ?. Você não poderia especificar 'What's your name ?' pois o Python não saberia que a segunda aspas não indica o fim da string. Você terá, então, que indicar isto ao Python. Isto pode ser feito com a ajuda das chamadas seqüências de escape. Utilizando seqüência de escape você especifica uma aspas simples como \' - observe a barra invertida. Assim nossa string ficaria assim: 'What\'s your name ?'

Outra maneira seria assim: ”What's your name ?” Da mesma maneira se você tivesse uma aspas dupla dentro desta string teria que usar a barra invertida. Para indicar a própria barra invertida você também tem que usar uma seqüência de escape: \\.

Se quiser especificar uma string de duas linhas? Você pode usar as aspas triplas como mostrado acima ou usar a seqüência de escape para o caracter de nova linha que é \n. Esta sequência de escape indica o início de outra linha. Exemplo: “Esta é a primeira linha.\nEsta é a segunda linha”. Outra seqüência de escape útil é a de tabulação: \t.

Uma barra invertida no final de uma linha indica que a string continua na outra linha, mas neste caso o caracter de nova linha não é inserido:

“Esta é a primeira linha da string. \
Aqui ainda é a primeira linha.”

Esta string é a mesma coisa que: 

“Esta é a primeira linha da string. Aqui ainda é a primeira linha”

Raw Strings

Se você não quiser que as seqüências de escape funcionem você deve definir a string como uma Raw String. Para isto basta preceder a string com r ou R. Exemplo:

r”Nas strings as novas linhas são indicadas por \n”

Strings são imutáveis

Em Python as strings são imutáveis, ou seja, uma vez criada a string não pode ser alterada. Isto pode parecer uma desvantagem mas não é. Veremos isto ao longo do estudo.

Concatenação de strings

Se você colocar duas strings lado a lado elas serão automaticamente concatenadas pelo Python. Por exemplo:

'Juntando' ' três ' 'strings'

é automaticamente convertido para:

'Juntando três strings'

Indexando strings

Em Python as strings podem ser indexadas; o primeiro caractere de uma string é indexado como zero. Substrings podem ser especificadas com a notação de dois índices separados pelo sinal de dois pontos.

samuel@aranha:~$ python
Python 2.3.5 (#2, Sep  4 2005, 22:01:42)
[GCC 3.3.5 (Debian 1:3.3.5-13)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> string = "Indexando strings com Python"
>>> string[0]
'I'
>>> string[1]
'n'
>>> string[2]
'd'
>>> string[0:9]
'Indexando'
>>> string[10:17]
'strings'
>>>
Se o primeiro índice for omitido o padrão será zero, se o segundo índice for omitido o padrão será o final da string.

>>> string[:17]
'Indexando strings'
>>> string[17:]
' com Python'
>>>

Strings Python não podem ser alteradas. Atribuir um valor a uma posição numa string resulta em um erro:

>>> string[17] = 'a'
Traceback (most recent call last):
File "<stdin>", line 1, in ?
TypeError: object doesn't support item assignment
>>>

Strins podem ser concatenadas. Para isto basta estarem lado a lado ou usar o operador +:

>>> 'Samuel' 'Dias' 'Neto'
'SamuelDiasNeto'
>>> 'Samuel' ' Dias' + ' Neto'
'Samuel Dias Neto'
>>> nome = 'Samuel Dias'
>>> nome + ' Neto'
'Samuel Dias Neto'
>>> nome[:8]
'Samuel D'
>>> nome[8:]
'ias'
>>> nome[:8] + nome[8:]
'Samuel Dias'
>>>

Índices incoerentes com o tamanho da string são tratados de forma especial. Um índice final maior que o tamanho da string é substituído pelo tamanho da string. Um índice final menor que o inicial retorna uma string vazia.

>>> nome[:100]
'Samuel Dias'
>>> nome[4:3]
''
>>>

Índices podem ser números negativos. Neste caso a contagem é iniciada a partir da direita. Por exemplo:

>>> nome
'Samuel Dias'
>>> nome[-1]
's'
>>> nome[-2]
'a'
>>> nome[-3]
'i'
>>> nome[-4]
'D'
>>> nome[-4:]
'Dias'
>>> nome[:-4]
'Samuel '
>>>

Mas observe que -0 é realmente o mesmo que 0, assim não conta a partir da direita!

>>> nome[0]
'S'
>>> nome[-0]
'S'
>>>

Índices negativos de tamanho maior que o tamanho da string são truncados, mas não tente isto com índices simples:

>>> nome[-100:]
'Samuel Dias'
>>> nome[-100]
Traceback (most recent call last):
File "<stdin>", line 1, in ?
IndexError: string index out of range
>>>

A melhor maneira de lembrar como estes índices trabalham é imaginá-los como apontadores que apontam para entre os caracteres, iniciando com o índice mais a esquerda numerado como zero. Assim, o índice mais a direita do último caractere de uma string de n caracteres tem índice n, por exemplo:

 +---+---+---+---+---+---+ 
 | S | a | m | u | e | l |  
 +---+---+---+---+---+---+ 
 0   1   2   3   4   5   6
-7  -6  -5  -4  -3  -2  -1
A primeira linha de números mostra a posição dos índices 0...6 na string; a segunda linha mostra os índices negativos correspondentes. O intervalo de i até j consiste em todos os caracteres entre os limites i e j respectivamente.

Para índices não negativos, o tamanho do intervalo é a diferença entre os índices, se ambos estiverem dentro dos limites. Por exemplo, o tamanho de word[1:3] é 2.

A função len() retorna o tamanho da string:

>>> nome
'Samuel Dias'
>>> len(nome)
11
>>>

Variáveis

Ao escrever programas para resolver problemas você terá que armazenar e manipular dados. Estes dados são armazenados utilizando as variáveis. Como o próprio nome diz, variáveis podem ter seu conteúdo alterado. Você pode armazenar qualquer coisa usando variáveis. Elas são apenas uma parte da memória do seu computador onde você armazena informações temporariamente. Para nomeá-las você deve observar as seguintes regras:

O primeiro caracter deve ser uma letra (maiúscula ou minúscula) ou o caracter de sublinhado ( _ );

O resto do nome pode conter letras (maiúsculas ou minúsculas), sublinhado ( _ ) ou dígitos (0-9);

Os nomes são sensíveis a caixa, ou seja “variavel” e “Variavel” não são a mesma coisa. Observe o primeiro v, no primeiro nome é minúsculo e no segundo é maiúsculo.

Exemplos de nomes de variáveis corretos são: nome, _idade, nome23, d3b1;

Exemplos de nomes de variáveis inválidos são: 2things, media aritmetica.

Objetos

Em Python tudo é considerado um objeto: números, strings, funções, etc... tudo é objeto. Isto pode não estar claro agora, mas guarde este conceito e no futuro você entenderá.

Usando variáveis

Abaixo segue um exemplo do uso de variáveis:

Usando variáveis

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# var.py
# exemplo do uso de variáveis

print "Números inteiros"
nr1 = 5
print nr1
nr1 = nr1 + 1
print nr1

print "Números de ponto flutuante"
nr2 = 96.5
print nr2
nr2 = nr2 + 0.25
print nr2

print 'Strings'
string = ''' Aqui temos uma string com mais de uma linha. Aqui é a primeira linha.
Aqui é a segunda linha.'''
print string

print '''
Observe que, no código fonte, as linhas iniciadas com # não executam nenhum comando pelo Python.
Elas são comentários. Toda linha que começa com # é um comentário.
A primeira linhas comentada é especial e indica o
programa a interpretar as linhas posteriores.
A segunda linha também é um comentários especial e indica o tipo
de caracteres que serão exibidos.
'''


Execução do programa:

samuel@aranha:~/python/scripts$ python var.py
Números inteiros
5
6
Números de ponto flutuante
96.5
96.75
Strings
Aqui temos uma string com mais de uma linha. Aqui é a primeira linha.
Aqui é a segunda linha.

Observe que, no código fonte, as linhas iniciadas com # não executam nenhum comando pelo Python.
Elas são comentários.
Toda linha que começa com # é um comentário.
A primeira linhas comentada é especial e indica o
programa que irá interpretar as linhas posteriores.
A segunda linha também é um comentários especial e indica o tipo
de caracteres que serão exibidos.

samuel@aranha:~/python/scripts$


Observe as linhas de comentário:

# var.py
# exemplo do uso de variáveis

Observe também que para executar o programa nós, agora, apenas o chamamos com o interpretador python:

python var.py

Esta é outra maneira de executar um programa Python.

Como o programa trabalha:

Primeiro nós atribuímos o valor 5 a variável nr1 usando o operador de atribuição =. Atribuir valores a variáveis é praticamente associar o valor a um nome. Em qualquer operação em meu programa onde houver a variável nr1, ela será substituída pelo valor 5. Depois ela foi exibida com o uso do comando print. Como já vimos, print exibe algo na tela. Depois ela foi usada numa operação de adição. Observe que como utilizamos o operador de atribuição novamente, agora a variável nr1 tem outro valor (nr1 + 1).

Da mesma forma atribuímos outros valores as outras variáveis e as exibimos na tela.

Linhas lógicas e linhas físicas

Uma linha física é o que você vê quando escreve o programa. Uma linha lógica é o que o Python entende como um simples comando. Python assume que cada linha física é uma linha lógica. Exemplo:

print “Alô Mundo!”

Esta é uma linha física que também é uma linha lógica. Python encoraja este tipo de utilização pois isto torna seu código mais fácil de ser entendido.

Se você quiser especificar mais de uma linha lógica numa só linha física deverá usar o ponto-e-vírgula para separar as linhas lógicas:

nr1 = 5; print nr1

Mas isto deve ser evitado.

É altamente recomendável que você utilize cada linha lógica em uma linha física para tornar seu código mais legível.

Indentação

Espaços em branco são importantes em Python. Os espaços em branco no início da linha são importantes. Isto é chamado indentação. Estes espaços deixados no início da linha são usados para determinar o nível de indentação da linha lógica o que, por sua vez, determina um grupo de comandos.

Isto significa que comandos do mesmo grupo devem ter a mesma indentação. Estes grupos de comandos relacionados e que tem a mesma indentação são chamados de blocos.

Indentação errada pode gerar erros. Exemplo:

#! /usr/bin/python
# -*- coding: iso-8859-1 -*-

# erro de indentação

nr = 7
 print 'O número vale',nr # observe o espaço no início desta linha
print 'Repetindo: o valor é',nr


Abaixo segue a execução do código acima:

samuel@aranha:~/python/scripts$ python indentacao.py
File "indentacao.py", line 7
print 'O número vale',nr # observe o espaço no início desta linha
^
SyntaxError: invalid syntax
samuel@aranha:~/python/scripts$


Observe o espaço em branco no início da penúltima linha do código. O erro indicado pelo Python diz que a sintaxe do programa está errada, isto é, o programa não foi escrito corretamente. A indentação deve ser usada apenas para destacar e organizar as instruções de um bloco de comandos e não em qualquer ocasião.

Não use uma mistura de tabulações e espaços para indentar seus códigos. Se você fizer isto seu código pode não trabalhar corretamente em outras plataformas. É altamente recomendável que você utilize apenas uma simples tabulação ou dois ou quatro espaços para cada nível de indentação. Escolha um destes estilos de indentação e use apenas ele.