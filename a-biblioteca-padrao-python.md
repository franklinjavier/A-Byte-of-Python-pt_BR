A biblioteca padrão Python

A biblioteca padrão é disponibilizada em toda instalação Python. Ela contém um grande número de módulos úteis. É importante você familiarizar-se com esta biblioteca pois a maioria dos seus problemas podem ser resolvidos utilizando seus módulos.

Exploraremos alguns dos módulos mais utilizados. Você pode encontrar informações detalhadas sobre todos os módulos na documentação oficial que vem com Python.

O módulo sys

O módulo sys contém funcionalidades específicas do sistema. Já vimos que sys.argv é uma lista que contém os argumentos passados na linha de comando.

Manipulando argumentos da linha de comando (sys.argv)

#!/usr/bin/python
#-*- coding: iso-8859-1 -*-

import sys

def readfile(filename):
  '''Imprime um arquivo na saída padrão.'''
  f = file(filename)
  while True:
    line = f.readline()
    if len(line) == 0:
      break
    print line, # observe a vírgula
    f.close()

# O script inicia aqui
if len(sys.argv) < 2:
  print 'Nenhuma ação especificada.'
  sys.exit()

if sys.argv[1].startswith('--'):
  option = sys.argv[1][2:]
  # pega sys.argv[1] sem os dois primeiros caracteres
  if option == 'version':
    print 'Versão 1.2'
  elif option == 'help':
    print '''\
Este programa exibe arquivos na saída padrão.
Qualquer número de arquivos podem ser especificados.
Opções:
  --version : Exibe a versão deste script
  --help : Exibe a ajuda'''
  else:
    print 'Opção desconhecida.'
    sys.exit()
else:
  for filename in sys.argv[1:]:
    readfile(filename)


Execução:

samuel@aranha:~/python/scripts$ python manipulando_args.py
Nenhuma ação especificada.
samuel@aranha:~/python/scripts$ python manipulando_args.py –help
Este programa exibe arquivos na saída padrão.
Pode ser passado mais de um arquivo.
Opções:
  --version : Exibe a versão deste script
  --help : Exibe a ajuda
samuel@aranha:~/python/scripts$ python manipulando_args.py –version
Versão 1.2
samuel@aranha:~/python/scripts$ python manipulando_args.py –opcao
Opção desconhecida.
samuel@aranha:~/python/scripts$ python manipulando_args.py teste.txt
Programar é divertido quando você termina o trabalho.
Se você quer fazer seu trabalho também divertido:
               use Python!
samuel@aranha:~/python/scripts$


Este programa tenta reproduzi o comportamento do comando cat já conhecido dos usuários Linux. Você apenas especifica os nomes de alguns arquivos texto e o programa os exibe na saída padrão.

Quando um programa Python está rodando, isto é, o interpretador não está em modo interativo, sempre existe, no mínimo, um item na lista sys.argv que é o nome do programa e este nome está disponível em sys.argv[0] uma vez que Python inicia a contagem a partir de zero. Os outros argumentos da linha de comando seguem este item.

Para tornar o programa mais amigável nós fornecemos algumas opções que o usuário pode especificar para aprender mais sobre o programa. Usamos o primeiro argumento para verificar se alguma destas opções foi passada. Se a opção passada foi --version, a versão do programa é exibida. Se a opção passada foi -- help, um pequeno texto de ajuda é exibido. Aqui nós usamos a função sys.exit para sair do programa. Para mais detalhes desta função veja help(sys.exit).

Quando nenhuma opção é especificada e nomes de arquivos são passados para o programa, ele simplesmente exibe cada linha dos arquivos. Os arquivos são lidos um após o outro.

Outros itens interessantes do módulo sys incluem sys.version que retorna a versão do interpretador Python, sys.stdin que corresponde a stream de entrada padrão, sys.stdout que corresponde a stream de saída padrão e sys.stderr que corresponde a stream de erro padrão.

O módulo os

Este módulo representa funcionalidades genéricas do sistema operacional. Ele é importante se você quer que seu programa seja independente de plataforma, isto é, ele permite que seu programa rode em Linux e Windows sem necessitar de nenhuma alteração. Um exemplo disto é usar a variável os.sep em vez de usar o caractere específico de separação do path do sistema operacional.

Abaixo temos a lista das partes mais importantes deste módulo:

os.name é uma string que especifica a plataforma que você está usando como “nt” para Windows e “posix” para Linux;

os.getcwd() é uma função que pega o diretório atual;

os.getenv() e os.putenv() são funções usadas para pegar e configurar variáveis de ambiente, respectivamente;

os.listdir() é uma função que retorna uma lista com os diretórios e arquivos de um diretório especificado;

os.remove() é uma função usada para remover um arquivo;

os.system() é uma função usada para rodar um comando shell;

os.linesep é uma string que retorna o terminador de linha da plataforma usada. Para Windows é '\r\n', para Linux é '\n' e para Mac é '\r';

os.path.split() é uma função que retorna o diretório e o arquivo de um path passado como argumento:

>>> os.path.split('/home/samuel/teste.txt')
('/home/samuel', 'teste.txt')
>>>

os.path.isfile() e os.path.isdir() são funções que verificam se um path passado como argumento refere-se a um arquivo ou a um diretório, respectivamente. Da mesma forma os.path.exists() verifica se um path existe.

Explore a documentação da linguagem para mais detalhes sobre estas funções e variáveis.