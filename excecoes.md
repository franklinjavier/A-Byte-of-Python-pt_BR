Exceções

Exceções ocorrem quando certas situações excepcionais ocorrem em seu programa. Como por exemplo, quando você está tentando abrir um arquivo e este não existe ou quando você apaga o arquivo enquanto o programa está rodando. Este tipo de situação é manipulada usando exceções.

O que acontece se seu programa tem alguma instrução inválida? Python identifica e lhe informa do erro.

Erros

Considere uma instrução print simples. O que acontece se digitarmos Print em vez de print? Observe o “p” maiúsculo. Python informa que houve um erro de sintaxe:

>>> Print 'Manipulando erros'
File "<stdin>", line 1
Print 'Manipulando erros'
                        ^
SyntaxError: invalid syntax
>>> print 'Manipulando erros'
Manipulando erros
>>>

Observe que é exibida uma mensagem indicando que o erro é de sintaxe: SyntaxError: invalid syntax. Além disso o local do erro é indicado: ^. É isto que um manipulador de erros faz.

Try.....Except

Tentaremos ler uma entrada do usuário.

>>> s = raw_input('Digite alguma coisa -->')
Digite alguma coisa -->

Neste ponto, em vez de digitar algo, pressione CTRL + D e veja o que acontece:

>>> s = raw_input('Digite alguma coisa -->')
Digite alguma coisa -->Traceback (most recent call last):
  File "<stdin>", line 1, in ?
EOFError
>>>

Python emite um erro chamado EOFError que basicamente significa que ele encontrou um fim de arquivo quando não esperava (o qual é representado pelo CTRL + D).

Agora veremos como manipular estes erros.

Manipulando exceções

No contexto Python erros são chamados de exceções. Podemos manipular exceções usando o comando Try.....Except. Basicamente colocamos todos os comandos e instruções num bloco Try e os manipuladores de erro num bloco Execpt.

Manipulando exceções

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

import sys

try:
  s = raw_input('Digite alguma coisa --> ')

except EOFError:
  print '\nPorque você emitiu um fim de arquivo?'
  sys.exit() # sai do prograga

except:
  print '\nOcorreu algum erro/exceção.'
  # Aqui nós não saímos do programa, houve um erro

print 'Feito'

Execução:

samuel@aranha:~/python/scripts$ python excecoes.py
Digite alguma coisa -->
Porque você emitiu um fim de arquivo?
samuel@aranha:~/python/scripts$ python excecoes.py
Digite alguma coisa --> Estou estudando Python
Feito
samuel@aranha:~/python/scripts$

Colocamos todos os comandos e instruções que podem emitir erro num bloco Try e manipulamos todos os erros em blocos Except. Uma cláusula Except pode manipular um simples erro/exceção ou uma lista de erros/exceções entre parênteses. Se nenhum nome de erro ou exceção for fornecido ela manipulará todos os erros. Deve haver pelo menos uma cláusula Except associada a cláusula Try.

Se algum erro ou exceção não for manipulado, o manipulador de erro padrão da linguagem Python é chamado. Ele apenas interrompe a execução do programa e emite uma mensagem como já vimos várias vezes.

Você também pode ter uma cláusula else associada com um bloco Try. A cláusula else é executada se não ocorrer nenhuma exceção.

Também podemos usar um objeto exceção e, assim, recuperar informação adicional sobre o erro. Isto é demonstrado no próximo exemplo.

Exceções definidas pelo usuário

Você pode definir suas próprias exceções. Para isto você define um objeto derivado da classe Error ou da classe Exception e depois usa o comando raise para capturar o erro e fazer a devida manipulação.

O comando raise permite ao programador forçar um determinado erro/exceção. Exemplo:

>>> raise NameError,'Palavra desconhecida'
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
NameError: Palavra desconhecida
>>>


O primeiro argumento de raise é o nome da exceção e o segundo argumento, que é opcional, especifica o argumento passado para a referida exceção. Vejamos um exemplo do uso de exceções definidas pelo usuário.

Exceção definida pelo usuário.

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

class PalavraPequena(Exception):
  '''Uma exceção definida pelo usuário.'''
  def __init__(self, tamanho, tamanho_minimo):
    Exception.__init__(self)
    self.tamanho = tamanho
    self.tamanho_minimo = tamanho_minimo

try:
  s = raw_input('Digite uma palavra --> ')
  if len(s) < 3:
    raise PalavraPequena(len(s), 3)

  # Aqui continuaria o processamento

except EOFError:
  print '\nPorque você emitiu um fim de arquivo?'

except PalavraPequena, x:
  print 'PalavraPequena: A palavra digitada tem %d caracteres \
enquanto o esperado era, no mínimo, %d' % (x.tamanho, x.tamanho_minimo)

else:
  print 'Não ocorreu nenhum erro.'


Execução:

samuel@aranha:~/python/scripts$ python raise.py
Digite uma palavra --> sa
PalavraPequena: A palavra digitada tem 2 caracteres enquanto o esperado era, no mínimo, 3
samuel@aranha:~/python/scripts$ python raise.py
Digite uma palavra --> sam
Não ocorreu nenhum erro.
samuel@aranha:~/python/scripts$ python raise.py
Digite uma palavra -->
Porque você emitiu um fim de arquivo?
samuel@aranha:~/python/scripts$


Aqui criamos a exceção PalavraPequena. Ela tem dois campos: tamanho que é o tamanho da string digitada pelo usuário e tamanho_minimo que é o tamanho mínimo desta string esperado pelo programa.

Na cláusula except, nós mencionamos a classe do erro e a variável que mantém o objeto erro/exceção correspondente. Isto é semelhante a parâmetros e argumentos numa chamada de função. Nesta cláusula except em particular, nós usamos os campos tamanho e tamanho_minimo do objeto exceção para emitir a devida mensagem ao usuário.

try.....finally

O que fazer se você está lendo um arquivo e quer fechá-lo, ocorra erro ou não? Isto pode ser feito usando um bloco finally. Observe que você pode usar uma cláusula except junto com um bloco finally no mesmo bloco try. Você terá que embutir um dentro do outro se quiser usar ambos.

Usando finally

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

import time

try:
  f = file('teste.txt')
  while True: # lendo um arquivo normalmente
    line = f.readline()
    if len(line) == 0:
      break
      time.sleep(2)
      print line,

finally:
  f.close()
  print 'Arquivo fechado!!!'


Execução:

samuel@aranha:~/python/scripts$ python finally.py
Programar é divertido quando você termina o trabalho.
Se você quer fazer seu trabalho também divertido:
Arquivo fechado!!!
Traceback (most recent call last):
  File "finally.py", line 12, in ?
      time.sleep(2)
KeyboardInterrupt
samuel@aranha:~/python/scripts$


Lemos o arquivo normalmente, introduzindo um tempo de espera de 2 segundos antes de exibir cada linha usando o método time.sleep. O programa, então, roda lentamente (Python é bem rápido por natureza). Quando o programa ainda estiver rodando, pressione Ctrl -c para interromper/cancelar o mesmo.

Observe que uma exceção KeyboardInterrupt é emitida e o programa encerrado, porém antes disto a cláusula finally é excutada e o arquivo fechado.