Mais Python

Até agora abordamos a maioria das características básicas da linguagem Python. Neste capítulo abordaremos alguns conhecimentos a mais, tornando seu aprendizado mais completo.

Métodos especiais

Existem alguns métodos que tem significado especial como os métodos __init__ e __del__ já vistos. Geralmente estes métodos são utilizados para imitar certos comportamentos. Por exemplo, se você quiser usar uma operação do tipo x[chave] em sua classe (como nas listas e tuplas), basta usar o método __getitem__(). É exatamente isto que Python faz com a classe list.

Alguns métodos especiais úteis são listados na tabela abaixo. Para ver a lista completa dos métodos especiais dê uma olhada no manual de referência da linguagem.

Alguns métodos especiais

Nome

Explicação

__init__(self,...)

Este método é chamado imediatamente antes do novo objeto criado ser retornado para uso.

__del__(self)

Chamado imediatamente antes do objeto ser destruído.

__str__(self)

Chamado quando usamos o comando print com o objeto ou quando str() é chamado.

__lt__(self,outro)

Chamado quando o operador menor que (<) é usado. Similarmente existem métodos especiais para todos os operadores (+, >, etc...).

__getitem__(self,chave)

Chamado quando uma operação do tipo x[chave] é usada.

__len__(self)

Chamado quando a função interna len() é usada.


Bloco de comando simples

Até agora observamos que os blocos de comando deve estar na próxima linha e com a mesma indentação. Porém, se seu bloco consiste de apenas uma linha há outra sintaxe disponível:

>>> flag=True
>>> if flag: print 'ok'
...
ok
>>>


Apesar de existir, é recomendável que você não use esta sintaxe.

Listas inteligentes

Listas inteligentes é uma técnica usada para criar listas a partir de outras. Por exemplo, você tem uma lista A de números e quer criar uma nova lista B composta pelos números de A multiplicados por dois, mas somente quando o número for maior que dois. A técnica das listas inteligentes é ideal para estas situações.

#!/usr/bin/python

lista_A = [2, 3, 4]
lista_B = [2*i for i in lista_A if i > 2]
print lista_B


Execução:

samuel@aranha:~/python/scripts$ python lista-inteligente.py
[6, 8]
samuel@aranha:~/python/scripts$


Aqui criamos uma nova lista especificando a manipulação a ser feita (2 * i) se uma condição for verdadeira (if i > 2). Observe que a lista original não é modificada. Muitas vezes utilizamos laços para processar os elementos de uma lista, porém o mesmo efeito pode ser conseguido usando esta técnica de listas inteligentes que é mais precisa, compacta e explícita.

Recebendo tuplas e listas em funções

Existe uma maneira especial de receber parâmetros para uma função como uma tupla ou dicionário usando os prefixos * ou **. Isto é útil quando precisamos passar uma quantidade variável de argumentos para uma função.

>>> def soma_de_potencias(potencia,*args):
...     '''Retorna a soma de cada argumento elevado a potencia.'''
...     total = 0
...     for n in args:
...          total += pow(n,potencia)
...     return total
...
>>> soma_de_potencias(2,3,4)
25
>>> soma_de_potencias(2,10)
100
>>>


Observe o prefixo * na variável args. Todos os argumentos passados para a função são armazenados em args como uma tupla. Se o prefixo ** for usado, os argumentos são considerados como pares chave/valor de uma dicionário.

lambda

O comando lambda é usado para criar novos objetos função e retorná-los em tempo de execução.

#!/usr/bin/python
#-*- coding: iso-8859-1 -*-

def repita(n):
  return lambda s: s * n

dois = repita(2)
print dois('palavra')
print dois(5)


Execução:

samuel@aranha:~/python/scripts$ python lambda.py
palavrapalavra
10
samuel@aranha:~/python/scripts$


Aqui usamos a função repita para criar novos objetos função em tempo de execução e retorná-los. o comando lambda é usado para criar o objeto função. Observe que lambda só pode conter expressões, nenhum outro comando pode existir nele, nem mesmo um simples print.

exec

O comando exec é usado para executar comandos Python armazenados numa string ou arquivo. Por exemplo, em tempo de execução você pode gerar uma string contendo um comando Python e executar este comando usando exec. Um simples exemplo é mostrado abaixo:

>>> c = "print 'Alô Mundo!'"
>>> exec c
Alô Mundo!
>>>


eval

O comando eval é usado para avaliar expressões Python válidas armazenadas numa string. Um simples exemplo é mostrado abaixo:

>>> e = "2 * 3"
>>> eval(e)
6
>>>


assert

O comando assert é usado para assegurar que algo é verdadeiro. Por exemplo, você precisa de, no mínimo, um elemento numa lista. Então, você quer checar isto e emitir um erro caso contrário. O comando assert é ideal para esta situação. Quando ele falha um erro AssertionError é emitido.

>>> lista=['sal']
>>> assert len(lista) >= 1
>>> lista.pop()
'sal'
>>> assert len(lista) >= 1
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
AssertionError
>>>


repr

A função repr é usada para obter uma representação string do objeto. Envolver o objeto em crases ( ` ) faz a mesma coisa. Observe que na maioria das vezes eval(repr(objeto)) == objeto.

>>> i = []
>>> i.append('item')
>>> `i`
"['item']"
>>> repr(i)
"['item']"
>>>


Basicamente a função repr ou as crases são usadas para obter uma representação imprimível do objeto. Você pode controlar o que seu objeto retorna para a função repr definindo o método __repr__ para sua classe.