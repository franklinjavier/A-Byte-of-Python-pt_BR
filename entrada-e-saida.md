Entrada/Saída

Muitas vezes você vai querer que seu programa interaja com o usuário (que pode ser você mesmo). Você pode querer pegar alguma informação do usuário e depois exibir algum resultado de volta. Podemos fazer isto usando raw_input e print, respectivamente. Para a saída também podemos usar os vários métodos da classe str (string). Por exemplo, você pode usar o método rjust para justificar uma string à esquerda. Veja help(str) para mais detalhes.

Outra maneira comum de entrada/saída é trabalhar com arquivos. A habilidade para criar, ler e escrever arquivos é essencial para muitos programas e exploraremos este aspecto neste capítulo.

Arquivos

Você pode abrir e usar arquivos para leitura e escrita criando um objeto da classe file e usando seus métodos read, readline ou write apropriadamente para ler ou escrever no arquivo. A habilidade para ler ou escrever no arquivo dependem do modo que você especificou ao abrir o arquivo. Finalmente, quando tiver terminado o trabalho com o arquivo, você deve chamar o método close para fechá-lo.

Usando arquivos

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

poem = '''\
Programr é divertido quando você termina o trabalho.
Se você quer fazer seu trabalho também divertido:
                 use Python!
'''

f = file('poem.txt', 'w') # abre para escrita ('w'riting)
f.write(poem) # escreve no arquivo
f.close() # fecha o arquivo

f = file('poem.txt') # se nenhum modo é especificado, o modo de
                     # escrita ('r'ead) é assumido por padrão
while True:
  line = f.readline()
  if len(line) == 0: # Zero indica fim de arquivo (EOF)
    break
  print line, # Observe a vírgula para evitar a adição automática
              # de um caractere de nova linha

f.close() # fecha o arquivo


Execução:

samuel@aranha:~/python/scripts$ python arquivos.py
Programar é divertido quando você termina o trabalho.
Se você quer fazer seu trabalho também divertido:
             use Python!
samuel@aranha:~/python/scripts$


Primeiro criamos uma instância da classe file, especificando o nome do arquivo e o modo de abertura. Os modos de abertura são: modo de leitura ('r'), modo de escrita ('w') e modo de adição ('a'). Atualmente existem outros modos disponíveis, help(file) lhe dará mais detalhes sobre eles.

Primeiro abrimos o arquivo em modo de escrita, usamos o método write para escrever nele e depois o fechamos com o método close.

Depois abrimos o mesmo arquivo para leitura. Se não especificamos o modo, o modo de leitura é assumido como padrão. Lemos cada linha do arquivo usando o método readline em um laço. Este método retorna uma linha inteira incluindo o caractere de nova linha. Quando uma string vazia é retornada, indica que o final do arquivo foi atingido e o laço é encerrado.

Observe que inserimos uma vírgula após print para suprimir o caractere de nova linha que normalmente é adicionado por este comando pois, a linha que é lida do arquivo já termina com um caractere de nova linha. Finalmente usamos close e fechamos o arquivo.

Pickle

Python fornece um método chamado Pickle que é usado para armazenar qualquer objeto num arquivo. Existe outro módulo chamado cPickle que funciona da mesma maneira que Pickle, exceto que, por ele ser escrito em C é muito mais rápido. Embora você possa usar qualquer um dos dois módulos, normalmente os dois são referenciados como Pickle.

Usando Pickle

#!/usr/bin/python
#-*- coding: iso-8859-1 -*-

# Usando Pickle

import cPickle as p
#import pickle as p

shoplistfile = 'shoplist.data' # arquivo onde armazenaremos
                                 o objeto

shoplist = ['apple', 'mango', 'carrot']

# Escrevendo no arquivo
f = file(shoplistfile, 'w')
p.dump(shoplist, f) 
f.close()

del shoplist # removendo shoplist

# Lendo o arquivo 
f = file(shoplistfile)
storedlist = p.load(f)
print storedlist


Execução:

samuel@aranha:~/python/scripts$ python pickle.py
['apple', 'mango', 'carrot']
samuel@aranha:~/python/scripts$


Primeiro observe que usamos a sintaxe import.....as. Isto é útil pois, assim podemos usar um nome curto para um módulo. Neste caso nós podemos podemos alternar entre os módulos cPickle e Pickle apenas alterando uma linha do código. No resto do programa nós nos referenciamos ao módulo apenas como “p”.

Para armazenar um objeto num arquivo, nós abrimos o arquivo em modo de escrita e chamamos o método dump do módulo Pickle. Este processo é chamado pickling.

Depois nós recuperamos o objeto usando o método load do módulo Pickle. Este processo é chamado unpickling.