Resolvendo um problema

Exploramos várias partes da linguagem Python. Agora juntaremos todas elas e escreveremos um programa que faz alguma coisa útil.

O problema

O problema é: Eu quero um programa que faça backup de todos meus arquivos importantes.

Embora seja um problema simples, não há informação bastante para iniciarmos a solução. Uma análise mais detalhada é requerida. Por exemplo, como especificaremos quais arquivos devem ser copiados? Onde o backup será armazenado? Como os arquivos serão armazenados?

Após analisar o problema nós já projetamos como será nosso programa. Faremos uma lista que descreve como nosso programa deverá trabalhar. É lógico que você pode ter outra solução e querer um programa que trabalhe diferente mas resolva o problema do mesmo jeito. Muitos problemas tem mais de uma maneira de ser resolvidos.

Os arquivos e diretórios a serem copiados serão especificados numa lista;

Os backups deverão ser armazenados num diretório principal de backup;

Os arquivos serão copiados num arquivo compactado;

O nome do arquivo de backup será a data hora de criação da cópia.

A solução

Como o projeto do nosso programa está concluído, agora podemos implementá-lo.

Script backup - primeira versão

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# backup1.py

import os
import time

# 1. Os arquivos e diretórios a serem copiados são especificados
# em uma lista
source = ['/home/python/scripts', '/home/sam/aprendendopython']
# Se você está usando Windows, use
# source = [r'C:\Documents', r'D:\Work'] ou algo parecido

# 2. O backup deve ser armazenado em um diretório principal
# de backup
target_dir = '/home/samuel/backup/'

# 3. Os arquivos são copiados para um arquivo zip.
# 4. O nome do arquivo zip é a data e hora atuais
target = target_dir + time.strftime('%Y%m%d%H%M%S') + '.zip'

# 5. Usamos o comando zip (em Unix/Linux) para compactar os arquivos
zip_command = "zip -qr '%s' %s" % (target, ' '.join(source))

# Rodando o backup
if os.system(zip_command) == 0:
  print 'Bakcup feito com sucesso para', target
else:
  print 'Erro ao tentar fazer backup!'


Execução:

samuel@aranha:~/python/scripts$ python backup1.py
Bakcup feito com sucesso para /home/samuel/backup/20060402144530.zip
samuel@aranha:~/python/scripts$


Agora estamos na fase de testes, onde testamos se nosso programa funciona corretamente. Se o comportamento não é o esperado, então temos que depurar o programa, isto é remover os bugs (erros).

Agora observaremos detalhadamente como convertemos nosso projeto em código.

Primeiro importamos os módulos os e time, pois eles serão usados. Depois especificamos os arquivos e diretórios a serem copiados na lista source. A variável target_dir refere-se ao diretório onde os arquivos de backup serão armazenados. O nome do arquivo de backup será a data e hora atuais, conseguimos isto através do uso da função time.strftime( ). O arquivo terá a extensão .zip pois será compactado neste formato. Juntamos o nome do diretório, o nome do arquivo e sua extensão e colocamos tudo na variável target. Ela então define o caminho completo para nosso arquivo de backup.

A função time.strftime( ) utiliza especificadores de formato como mostrado no exemplo. A especificação %Y será substituída pelo ano. A especificação %m será substituída pelo mês como um número entre 01 e 12. a lista completa destas especificações podem ser encontradas no Manual de Referência do Python que normalmente vem junto com o Python. Observe que estas especificações são parecidas com aquelas usadas com o comando print (quando este vem seguido de % e de uma tupla).

Nós criamos o nome do arquivo de cópia com o operador '+' que concatena strings, isto é, ele junta as strings usadas como operandos e retorna uma única string. Então, criamos a string zip_command que contém o comando que iremos executar. Podemos checar se este comando trabalha corretamente executando-o num shell.

O comando zip usado recebeu alguns argumentos. A opção -q é usada para indicar que o comando zip deve trabalhar quieto, isto é, sem emitir nenhuma mensagem. A opção -r especifica que o zip deve trabalhar recursivamente, ou seja, deve incluir os subdiretórios e seus arquivos no arquivo de cópia criado. As duas opções são combinadas e passadas como -qr. As opções são seguidas pelo nome do arquivo zip a ser criado e pela lista de arquivos e diretórios a serem copiados. Convertemos a lista source em uma string usando o método join, já visto.

Então, finalmente rodamos o comando com a função os.system que executa um comando como se ele estivesse sendo rodado a partir do shell. Ela retorna zero se o comando for executado com sucesso. Caso contrário, retorna um número de erro.

Dependendo da saída do comando, nós exibimos uma mensagem dizendo se o backup foi executado com sucesso ou não.

Agora que temos o script de backup funcionando podemos fazer cópias dos nossos arquivos importantes. Usuários Linux podem conceder permissão de execução ao script e colocá-lo no PATH para que seja executado a partir de uma chamada do shell. Esta fase é chamada fase de operação ou fase de distribuição do software.

Apesar do programa acima trabalhar corretamente, normalmente os primeiros programas não trabalham bem. Por exemplo, podem ocorrer problemas se você não projetou o programa direito ou se você errou ao digitar o código. Caso isto ocorra você deverá voltar a fase de projeto ou deverá depurar o programa.

Segunda versão

A primeira versão do nosso script trabalha, porém podemos fazer alguns refinamentos de modo que ele trabalhe melhor. Esta fase é chamada fase de manutenção do software.

Um dos refinamentos úteis seria um mecanismo de nomeação melhor, como por exemplo, usar a hora como nome do arquivo, dentro de um diretório nomeado com a data atual e este diretório dentro do diretório principal de backup. Uma vantagem disto é que seus backups seriam armazenados de forma hierárquica e isto facilitaria o gerenciamento destes arquivos. Outra vantagem é que os nomes dos arquivos seriam bem menores. Outra vantagem seria que diretórios separados para cada dia tornariam fácil checar se houve o backup em determinado dia, uma vez que o diretório só poderia ser criado se você tivesse feito o backup naquele dia.

Script backup - segunda versão

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# backup2.py

import os
import time

# 1. Os arquivos e diretórios a serem copiados são especificados
# em uma lista
source = ['/home/python/scripts', '/home/sam/aprendendopython']
# Se você está usando Windows, use
# source = [r'C:\Documents', r'D:\Work'] ou algo parecido

# 2. O backup deve ser armazenado em um diretório principal de backup
target_dir = '/home/samuel/backup/'

# 3. Os arquivos são copiados para um arquivo zip.
# 4. O dia atual é o nome do subdiretório onde será armazenado o backup
hoje = target_dir + time.strftime('%Y%m%d')
# A hora atual é o nome do arquivo zip
agora = time.strftime('%H%M%S')

# se o subdiretório não existir ele será criado
if not os.path.exists(hoje):
  os.mkdir(hoje) # cria o subdiretório
  print 'Subdiretório',hoje,'criado com sucesso'

# nome do arquivo de cópia
target = hoje + os.sep + agora + '.zip'

# 5. Usamos o comando zip (em Unix/Linux) para compactar os arquivos
zip_command = "zip -qr '%s' %s" % (target, ' '.join(source))

# Rodando o backup
if os.system(zip_command) == 0:
  print 'Bakcup feito com sucesso para', target
else:
  print 'Erro ao tentar fazer backup!'


Execução:

samuel@aranha:~/python/scripts$ python backup2.py
Subdiretório /home/samuel/backup/20060408 criado com sucesso
Bakcup feito com sucesso para /home/samuel/backup/20060408/045108.zip
samuel@aranha:~/python/scripts$


A maior parte do programa é igual a primeira versão. A diferença é que checamos se existe, dentro do diretório principal de backup, um subdiretório cujo nome seja a data atual. Para isto usamos a f unção os.exists. Se o subdiretório não existe, nós o criamos com a função os.mkdir.

Observe o uso da variável os.sep. Ela fornece o caractere separador de diretórios de acordo com seu sistema operacional, isto é, '/' para Linux/Unix, '\\' para Windows e ':' para Mac OS. Usar os.sep em vez destes caracteres diretamente torna seu código portável de modo que seu programa trabalhará corretamente em todas estas plataformas.

Terceira versão

A segunda versão trabalham bem, porém ainda temos dificuldade de identificar o conteúdo dos arquivos de backup. Por exemplo, eu posso fazer alterações em algum programa ou apresentação e querer que o nome do arquivo de backup referencie de alguma maneira estas alterações. Isto pode ser facilmente conseguido solicitando do usuário o comentário a ser inserido no nome do arquivo.

Script backup – terceira versão (esta não trabalha)

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# backup3.py

import os
import time

# 1. Os arquivos e diretórios a serem copiados são especificados
# em uma lista
source = ['/home/python/scripts', '/home/sam/aprendendopython']
# Se você está usando Windows, use
# source = [r'C:\Documents', r'D:\Work'] ou algo parecido

# 2. O backup deve ser armazenado em um diretório principal de backup
target_dir = '/home/samuel/backup/'

# 3. Os arquivos são copiados para um arquivo zip.
# 4. O dia atual é o nome do subdiretório onde será armazenado o backup
hoje = target_dir + time.strftime('%Y%m%d')
# A hora atual é o nome do arquivo zip
agora = time.strftime('%H%M%S')

# Pegando o comentário do usuário para criar o nome do arquivo
comentario = raw_input('Entre com o comentário --> ')
if len(comentario) == 0: # checando se o comentário foi fornecido
  target = hoje + os.sep + agora + '.zip'
else:
  target = hoje + os.sep + agora + '_' +
  comentario.replace(' ', '_') + '.zip'

# se o subdiretório não existir ele será criado
if not os.path.exists(hoje):
  os.mkdir(hoje) # cria o subdiretório
  print 'Subdiretório',hoje,'criado com sucesso'

# 5. Usamos o comando zip (em Unix/Linux) para compactar os arquivos
zip_command = "zip -qr '%s' %s" % (target, ' '.join(source))

# Rodando o backup
if os.system(zip_command) == 0:
  print 'Bakcup feito com sucesso para', target
else:
  print 'Erro ao tentar fazer backup!'


Execução:

samuel@aranha:~/python/scripts$ python backup3.py
  File "backup3.py", line 27
    target = hoje + os.sep + agora + '_' +
                                         ^

SyntaxError: invalid syntax
samuel@aranha:~/python/scripts$


Este programa não trabalha corretamente! O Python diz que há um erro de sintaxe, o que significa que o script não satisfaz a estrutura que o Python espera ver. Observando a mensagem de erro emitida pelo Python também podemos ver onde o erro ocorreu. Então, iniciamos depurando nosso programa nesta linha.

Uma observação cuidadosa mostra que uma linha lógica foi dividida em duas linhas físicas e não foi indicado ao Python que estas linhas físicas são uma única linha lógica. Basicamente o Python encontrou o operador de adição ( + ) faltando um operando e não sabe o que fazer. Lembre-se que podemos especificar que a linha lógica continua na próxima linha através da inserção de um caractere de barra invertida ao final da linha. Então fazemos esta correção em nosso programa. Isto é chamado corrigir o bug.

Quarta versão

Script backup – quarta versão

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# backup4.py

import os
import time

# 1. Os arquivos e diretórios a serem copiados são especificados
# em uma lista
source = ['/home/python/scripts', '/home/sam/aprendendopython']
# Se você está usando Windows, use
# source = [r'C:\Documents', r'D:\Work'] ou algo parecido

# 2. O backup deve ser armazenado em um diretório principal de backup
target_dir = '/home/samuel/backup/'

# 3. Os arquivos são copiados para um arquivo zip.
# 4. O dia atual é o nome do subdiretório onde será armazenado o backup
hoje = target_dir + time.strftime('%Y%m%d')
# A hora atual é o nome do arquivo zip
agora = time.strftime('%H%M%S')

# Pegando o comentário do usuário para criar o nome do arquivo
comentario = raw_input('Entre com o comentário --> ')
if len(comentario) == 0: # checando se o comentário foi fornecido
  target = hoje + os.sep + agora + '.zip'
else:
  target = hoje + os.sep + agora + '_' + \
  comentario.replace(' ', '_') + '.zip'

# se o subdiretório não existir ele será criado
if not os.path.exists(hoje):
  os.mkdir(hoje) # cria o subdiretório
  print 'Subdiretório',hoje,'criado com sucesso'

# 5. Usamos o comando zip (em Unix/Linux) para compactar os arquivos
zip_command = "zip -qr '%s' %s" % (target, ' '.join(source))

# Rodando o backup
if os.system(zip_command) == 0:
  print 'Bakcup feito com sucesso para', target
else:
  print 'Erro ao tentar fazer backup!'


Execução:

samuel@aranha:~/python/scripts$ python backup4.py
Entre com o comentário --> quarta versao
Bakcup feito com sucesso para /home/samuel/backup/20060411/053137_quarta_versao.zip
samuel@aranha:~/python/scripts$


Este programa agora trabalha. Pegamos o comentário do usuário com a função raw_input()então verificamos se o usuário digitou alguma coisa analisando o resultado da função len(). Se o usuário não digitou nada fazemos o backup como antes. Porém, se um comentário foi fornecido, ele é anexado ao nome do arquivo antes da extensão .zip. Observe que substituímos os espaços entre as palavras do comentário pelo caractere de sublinhado. Isto porque gerenciar arquivos com nomes assim é mais fácil.

Mais refinamentos

A quarta versão trabalha bem, porém, sempre existem aperfeiçoamentos que podem ser inseridos. Por exemplo, você pode incluir a opção -v para que seu programa emita mensagens que indicam como o trabalho está sendo feito.

Outro aperfeiçoamento seria a passagem de arquivos e diretórios para o script na linha de comando. Podemos pegar estes argumentos de linha de comando através da lista sys.argv e podemos adicioná-los a nossa lista source utilizando o método extend da classe lista.

Outro refinamento que eu gosto é usar o comando tar em vez do comando zip. Uma das vantagens é que usando tar o bakcup é mais rápido e o arquivo criado é menor. Se eu precisar manipular o arquivo de cópia no Windows, o WinZip trabalha bem com arquivos .tar.gz. A maioria das distribuições Linux já vem com o tar. Usuários windows podem baixar a partir de http://gnuwin32.sourceforge.net/packages/tar.htm.

O comando para compactar agora será:

tar = 'tar -cvzf %s %s -X /home/swaroop/excludes.txt' % (target, ' '.join(srcdir))

As opções são explicadas abaixo:

-c indica a criação de um arquivo;

-v indica verbose, isto é, o comando emitirá mensagens indicando como o trabalho está sendo feito;

-z indica que o filtro gzip deve ser usado;

-f indica que deve ser forçada a criação do arquivo, isto é, se já existir será substituído;

-X indica uma lista de arquivos que devem ser excluídos do backup. Por exemplo, você pode especificar *~ para não incluir os arquivos terminados em ~ no seu backup.

IMPORTANTE: A melhor maneira de se criar arquivos compactados é usando os módulos zipfile e tarfile. Eles fazem parte da biblioteca padrão do Python e já vem pronto para você usar. Usar estas bibliotecas também evita o uso de os.system, o que é contra-indicado pois é muito fácil cometer erros usando-o.

Conclusão: o processo de desenvolvimento de um programa

Durante a construção do nosso script de backup vimos as várias fases no processo de desenvolvimento de um programa. Estas fases podem ser resumidas assim:

O que fazer (Análise do problema);

Como fazer (Projeto);

Criação (Implementação);

Teste (Testar e depurar);

Uso (Usar e distribuir);

Manutenção (Refinamentos)

Uma maneira recomendada para escrever programas é seguir como fizemos para criar nosso script de backup. Analisar o problema e fazer um projeto. Iniciar a implementação com uma versão bem simples. Testar e depuar esta versão. Usá-la para garantir que trabalha corretamente. Agora adicionar mais recursos e repetir o ciclo criar-testar-usar quantas vezes for necessário. Lembre-se que o software deve ir crescendo aos poucos e não ser criado de uma só vez com todos seus recursos.