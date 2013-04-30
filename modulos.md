Módulos

Você viu como reutilizar código através do uso de funções. E se você quiser usar suas funções em outros programas que você escrever? Como você deve estar pensando, a resposta é utilizar módulos. Um módulo basicamente é um arquivo contendo funções e variáveis que você definiu. Para reutilizar o módulo em outros programas o arquivo deve ter uma extensão .py.

Usando módulos da biblioteca padrão

Um módulo pode ser importado por outro programa para que este possa fazer uso da sua funcionalidade. É desta maneira que utilizamos a biblioteca padrão do Python. Primeiro veremos como usar os módulos da biblioteca padrão.

Usando o módulo sys

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando o módulo sys

import sys

print 'Os argumentos passados para a linha de comando são:'
for i in sys.argv:
  print i

print '\n\nO PYTHONPATH é', sys.path, '\n'


Execução:

samuel@aranha:~/python/scripts$ python modulo1.py inserindo sys 38 1967
Os argumentos passados para a linha de comando são:
modulo1.py
inserindo
sys
38
1967



O PYTHONPATH é ['/home/samuel/python/scripts', '/usr/lib/python23.zip', '/usr/lib/python2.3', '/usr/lib/python2.3/plat-linux2', '/usr/lib/python2.3/lib-tk', '/usr/lib/python2.3/lib-dynload', '/usr/local/lib/python2.3/site-packages', '/usr/lib/python2.3/site-packages']

samuel@aranha:~/python/scripts$


Primeiro nós importamos o módulo sys usando o comando import. Basicamente este comando diz ao Python que queremos usar este módulo. O módulo sys contém funcionalidades relacionadas ao interpretador Python e seu ambiente.

Quando o executa o comando import sys ele procura pelo módulo sys.py em um dos diretórios listados em sua variável sys.path. Se o arquivo é encontrado, os comandos do bloco principal do módulo são rodados e o módulo torna-se disponível para seu uso. Observe que a inicialização é feita somente na primeira vez que importamos um módulo. 'sys' neste caso é a abreviatura de 'system'.

A variável argv do módulo sys é referenciada usando a notação sys.argv . Uma das vantagens desta abordagem é que o nome não conflitará com nenhuma variável local de nome argv usada em seu programa. Além disso esta nomenclatura indica claramente que este nome é parte do módulo sys.

A variável sys.argv é uma lista de strings (listas serão explanadas mais a frente). Especificamente, sys.argv contém a lista dos argumentos passados na linha de comando.

O Python armazena o nome do script como primeiro argumento da lista sys.argv, no caso sys.argv[0]; o segundo argumento é armazenado em sys.argv[1], o terceiro em sys.argv[2], e assim por diante. Isto ficará mais claro ao estudarmos as listas.

sys.path contém a lista de diretórios de onde os módulos são importados. Note que a primeira string em sys.path é vazia. Esta string vazia indica que o diretório corrente também é parte de sys.path. Isto significa que você pode importar módulos localizados no diretório corrente. Caso seu módulo não esteja no diretório corrente você terá que colocá-lo em um dos diretórios listados em sys.path.

Arquivos .pyc

Importar um módulo é uma operação lenta porém, o Python tem alguns truques para tornar isto mais rápido. Uma das maneiras é criar arquivos com a extensão .pyc . Este arquivo será útil na próxima vez que você importar o módulo. Esta importação será muito mais rápida já que parte do processamento requerido para importar o módulo já foi feito. Você não precisa fazer nada, o próprio Python se encarrega de criar os arquivos .pyc . Estes arquivos são independentes de plataforma.

from.....import

Se você quiser importar a variável argv diretamente para seu programa (e evitar digitar sys. toda vez), então você pode usar o comando from sys import argv. Se você quer importar todos os nomes do módulo sys, pode usar o comando from sys import *. Este comando funciona com qualquer módulo. De forma geral evite usar o comando from......import. Prefira o comando import pois assim seus códigos ficarão mais legíveis e evitarão conflitos de nomes.

__name__

Todo módulo tem um nome e os comandos do módulo podem encontrar este nome. Isto é especialmente útil numa situação particular – como mencionado anteriormente quando um módulo é importado pela primeira vez, seu bloco principal é rodado. E se nós só quisermos executar o bloco principal se o módulo estiver sendo executado ele mesmo e não sendo importado? Isto pode ser conseguido utilizando o atributo __name__ do módulo.

Usando __name__

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando o atributo __name__ de um módulo

if __name__ == '__main__':
  print 'Este programa está rodando isoladamente'
else:
  print 'Estou sendo importado por outro módulo'


Execução:

samuel@aranha:~/python/scripts$ python modulo2.py
Este programa está rodando isoladamente


samuel@aranha:~/python/scripts$ python
Python 2.3.5 (#2, Sep 4 2005, 22:01:42)
[GCC 3.3.5 (Debian 1:3.3.5-13)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import modulo2
Estou sendo importado por outro módulo
>>>


Todo módulo Python tem seu __name__ definido e se este é '__main__', isto significa que o programa está sendo rodado diretamente pelo usuário e não importado por outro programa.

Criando módulos

Criar módulos é fácil, você tem feito isto durante todo estudo deste livro. Todo programa Python também é um módulo. Você apenas tem que certificar-se que ele tem a extensão .py . O exemplo seguinte tornará este conceito mais claro:

Criando um módulo

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# criando um módulo de nome meumodulo.py

def oi():
  print 'Oi, este é meu módulo.'

versao = '0.1'

# Fim do meumodulo.py


Acima temos um módulo. Como você pode ver, ele não tem nada de diferente de um programa Python comum. Veremos como usar este módulo em outros programas Python.

Lembre-se que o módulo ou deve estar no mesmo diretório do programa que vai importá-lo ou deve estar num dos diretório listados em sys.path.

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando o meumodulo.py

import meumodulo

meumodulo.oi()
print 'Versão',meumodulo.versao


Execução:

samuel@aranha:~/python/scripts$ python usando_meumodulo.py
Oi, este é meu módulo.
Versão 0.1
samuel@aranha:~/python/scripts$


Observe que sempre usamos uma mesma sintaxe do tipo módulo.objeto para acessar objetos do módulo. Isto é uma das coisas boas do Python. A utilização da mesma sintaxe é o jeito Python de fazer as coisas e isto evita que tenhamos que aprender novas maneiras para fazer coisas semelhantes.

A função dir( )

Você pode usar a função interna dir( ) para listar os identificadores que um módulo define. Os identificadores são as funções, classes e variáveis definidas no módulo.

Quando você fornece o nome de um módulo para a função dir( ), ela retorna a lista dos nomes definidos no referido módulo. Quando nenhum argumento é passado ela retorna a lista dos nomes definidos no módulo corrente.

Usando a função dir( )

samuel@aranha:~$ python
Python 2.3.5 (#2, Sep 4 2005, 22:01:42)
[GCC 3.3.5 (Debian 1:3.3.5-13)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> dir(sys) # pega a lista de atributos do módulo sys
['__displayhook__', '__doc__', '__excepthook__', '__name__', '__stderr__', '__stdin__', '__stdout__', '_getframe', 'api_version', 'argv', 'builtin_module_names', 'byteorder', 'call_tracing', 'callstats', 'copyright', 'displayhook', 'exc_clear', 'exc_info', 'exc_type', 'excepthook', 'exec_prefix', 'executable', 'exit', 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags','getfilesystemencoding', 'getrecursionlimit', 'getrefcount', 'hexversion', 'maxint', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks', 'path_importer_cache', 'platform', 'prefix','ps1', 'ps2', 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit', 'settrace', 'stderr', 'stdin', 'stdout', 'version', 'version_info', 'warnoptions']
>>>
>>> a = 5 # cria uma nova variável a
>>> dir()
['__builtins__', '__doc__', '__name__', 'a', 'sys']
>>>
>>> del a # apaga a variável a
>>> dir()
['__builtins__', '__doc__', '__name__', 'sys']
>>>


Primeiro usamos dir( ) com o módulo importado sys. Observe que todos os identificadores de sys foram exibidos.

Depois usamos dir( ) sem nenhum argumento e a lista dos identificadores do módulo corrente foi exibida. Observe que a lista contém inclusive o módulo sys que foi importado. Os módulos importados também fazem parte da lista retornada por dir( ).

Para observar dir( ) em ação criamos uma variável e chamados dir( ) novamente. Podemos ver que esta nova variável foi listada. Depois removemos a mesma e ela não mais aparece na lista de identificadores retornada por dir( ).

OBSERVAÇÃO: o comando del é usado para apagar uma variável/nome.