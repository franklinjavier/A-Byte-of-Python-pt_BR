Estruturas de dados

Estruturas de dados são utilizadas para armazenar coleções de dados relacionados. Existem três estruturas de dados internas no Python: listas, tuplas e dicionários. Veremos agora como utilizá-las e como elas tornam nossa vida mais fácil.

Listas

Uma lista nada mais é que uma lista ordenada de itens, como o próprio nome indica. Ou seja, você pode armazenar uma seqüência de itens numa lista. É fácil visualizar uma lista, lembra daquela velha lista de compras que você escreve quando vai ao supermercado? Uma lista é assim. A diferença é que provavelmente sua lista de compras deve ter um item em cada linha, enquanto que uma lista do Python tem os itens lado a lado, separados por vírgula.

A lista deve estar entre colchetes, assim o Python entende que você está especificando uma lista. Uma vez que você tenha criado a lista, você pode adicionar, remover ou procurar itens nela. Como podemos adicionar e remover itens da lista dizemos que a lista é um tipo de dados mutável, isto é, um tipo de dados que pode ser alterado.

Uma rápida introdução a objetos e classes

Embora eu tenha atrasado a discussão sobre objetos e classes até agora, uma pequena explicação é necessária para que você possa entender melhor as listas. Nós ainda exploraremos este tópico em detalhes em seu próprio capítulo.

Uma lista é um exemplo do uso de objetos e classes. Quando você cria uma variável i e atribui a ela um valor inteiro 5, você acabou de criar o objeto (instância) i da classe (tipo) inteiro. Você pode confirmar isto e entender melhor dando uma olhada em help(int).

Uma classe pode ter métodos, que são funções definidas para uso somente com a referida classe. Você só pode usar a funcionalidade dos métodos quando tem um objeto da referida classe. Por exemplo, o Python fornece um método chamado append para a classe lista que permite adicionar um item ao final da lista. A instrução minha_lista.append(“um item”) adicionará a string a lista minha_lista. Observe o uso da sintaxe objeto.método para acessar os métodos dos objetos.

Uma classe também pode ter campos que nada mais são que variáveis definidas para uso somente com a referida classe. Você só pode usar estas variáveis/nomes quando tiver um objeto da referida classe. Os campos são acessados usando a mesma sintaxe dos métodos: lista.campo.

Usando listas

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando listas

# Esta é minha lista de compras
shoplist = ['maçã', 'banana', 'mamão', 'uva']

print 'Tenho ', len(shoplist), 'items a serem comprados.'

print 'Estes itens são:', # Observe a vírgula no final da linha
for item in shoplist:
  print item,

print '\nTambém tenho que comprar goiaba.'
shoplist.append('goiaba')

print 'Minha lista de compras agora é', shoplist

print 'Agora organizarei minha lista'
shoplist.sort()

print 'Minha lista organizada é', shoplist

print 'O primeiro item que comprarei é', shoplist[0]

olditem = shoplist[0]
del shoplist[0]
print 'Já comprei', olditem
print 'Minha lista agora é', shoplist

olditem = shoplist[0]
del shoplist[0]
print 'Já comprei', olditem
print 'Minha lista agora é', shoplist

olditem = shoplist[0]
del shoplist[0]
print 'Já comprei', olditem
print 'Minha lista agora é', shoplist


Exemplo:

samuel@aranha:~/python/scripts$ python lista.py
Tenho 4 items a serem comprados.
Estes itens são: maçã banana mamão uva
Também tenho que comprar goiaba.
Minha lista de compras agora é ['ma\xe7\xe3', 'banana', 'mam\xe3o', 'uva', 'goiaba']
Agora organizarei minha lista
Minha lista organizada é ['banana', 'goiaba', 'mam\xe3o', 'ma\xe7\xe3', 'uva']
O primeiro item que comprarei é banana
Já comprei banana
Minha lista agora é ['goiaba', 'mam\xe3o', 'ma\xe7\xe3', 'uva']
Já comprei goiaba
Minha lista agora é ['mam\xe3o', 'ma\xe7\xe3', 'uva']
Já comprei mamão
Minha lista agora é ['ma\xe7\xe3', 'uva']
samuel@aranha:~/python/scripts$


A variável shoplist é uma lista de compras de alguém que está indo ao mercado. Em shoplist nós só armazenamos strings com os nomes dos produtos a serem comprardos, mas lembre-se que você pode armazenar qualquer tipo de objeto numa lista, inclusive números e até mesmo outras listas.

Também usamos um laço for.....in para iterar sobre os itens da lista. Por enquanto aceite que uma lista é também uma seqüência. As seqüências serão abordadas mais a frente.

Observe que colocamos uma vírgula ao final do comando print para suprimir o caractere de nova linha que é automaticamente colocado no final de todo comando print.

Depois adicionamos um item a lista usando o método append do objeto lista, como discutido antes. Depois checamos se o item foi realmente adicionado através da exibição do conteúdo da lista. Isto foi feito pela passagem da lista para o comando print.

Então organizamos a lista utilizando o método sort do objeto lista. Entenda que este método afeta a própria lista e não retorna uma lista modificada. Isto difere da maneira que as strings trabalham. É por isso que dizemos que as listas são mutáveis e as strings imutáveis.

Depois, quando compramos um determinado item no mercado queremos excluí-lo da lista. Fazemos isto utilizando o comando del. Aqui especificamos qual item da lista queremos que seja removido e del faz isto para nós. No caso especificamos o primeiro item da lista. Para isto usamos o comando del shoplist[0] (lembre-se que Python inicia a contagem a partir de zero).

Indexando listas

Assim como as strings, as listas também podem ser indexadas.

>>> lista = ['python',35,14.0,'string']
>>> lista
['python', 35, 14.0, 'string']
>>> lista[1]
35
>>> lista[2]
14.0
>>> lista[0]
'python'
>>> lista[1:]
[35, 14.0, 'string']
>>> lista[:2]
['python', 35]
>>>


Métodos do objeto lista

Para ver todos os métodos do objeto lista execute help(list) no interpretador Python. Abaixo segue a lista deles.

append(x)

Adicona um item ao fim da lista; equivale a a[len(a):] = [x].
extend(L)

Estende a lista pela adição de todos os itens em uma lista dada; equivale a a[len(a):] = L.
insert(i, x)

Insere um item em uma determinada posição. O primeiro argumento é o índice do elemento anterior a posição da inserção, assim a.insert(0, x) insere no início da lista, e a.insert(len(a), x) equivale a a.append(x).
remove(x)

Remove o primeiro item da lista cujo valor é x. Se não existe tal item ocorre um erro.
pop([i])

Remove o item de uma dada posição da lista e o retorna. Se nenhum índice é especificado, a.pop() retorna o último item da lista. O item é também removido da lista. (Os colchetes envolvendo o i na assinatura do método denota que o parâmetro é opcional, não que você deve digitar colchetes nesta posição. Você encontra esta notação freqüentemente na documentação oficial do Python.
index(x)

Retorna o índice do primeiro item cujo valor é x. Se não existir tal item ocorre um erro.
count(x)

Retorna o número de vezes que x aparece na lista.
sort()

Organiza os itens da lista.
reverse()

Reorganiza os elementos da lista em ordem decrescente.
Tuplas

Tuplas são semelhantes a listas, porém elas são imutáveis como as strings. Então você não pode modificar as tuplas. Elas são definidas com seus elementos separados por vírgula dentro de parêntees.

Usando tuplas

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando tuplas

zoo = ('lobo', 'elefante', 'pingüim')
print 'O número de animais do zoológico é', len(zoo)
novo_zoo = ('macaco','golfinho',zoo)
print 'O número de animais do novo zoológico é', len(novo_zoo)
print 'Todos os animais do novo zoológico são', novo_zoo
print 'Animais comprados do velho zoológico', novo_zoo[2]
print 'Últimos animais comprados do velho zoológico ;', novo_zoo[2][2]


Execução:

samuel@aranha:~/python/scripts$ python tupla.py
O número de animais do zoológico é 3
O número de animais do novo zoológico é 3
Todos os animais do novo zoológico são ('macaco', 'golfinho', ('lobo', 'elefante', 'ping\xfcim'))
Animais comprados do velho zoológico ('lobo', 'elefante', 'ping\xfcim')
Últimos animais comprados do velho zoológico ; pingüim
samuel@aranha:~/python/scripts$


A variável zoo refere-se a uma tupla de itens. Vemos que a função len( ) pode ser usada para pegar o tamanho da tupla. Isto indica que a tupla também é uma seqüência.

Estamos a agora deslocando estes animais para um novo zoológico e o antigo será fechado. Então, a tupla novo_zoo contém os novos animais comprados e os animais do antigo zoológico. Observe que as tuplas podem estar aninhadas, ou seja, uma dentro da outra.

Nós podemos acessar os itens de uma tupla com a mesma sintaxe que acessamos os itens numa lista. Acessamos o terceiro item da tupla novo_zoo especificando novo_zoo[2] e acessamos o terceiro item do terceiro item de novo_zoo especificando novo_zoo[2][2].

Tupla com 0 ou 1 item. Uma tupla vazia é construída com um par de parênteses vazio, assim: tuplavazia = ( ). Uma tupla com um item apenas deve ter o referido item seguido por uma vírgula: tuplasimples = (2,).

Tuplas e o comando print

Um dos usos mais comuns da tupla é em conjunto com o comando print. Exemplo;

Saída usando tuplas e print

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# saída usando tuplas e print

idade = 38
nome = 'Samuel'

print '%s : %d anos' % (nome, idade)
print 'Programado por: %s' % nome


Execução:

samuel@aranha:~/python/scripts$ python tuplas+print.py
Samuel : 38 anos
Programado por: Samuel
samuel@aranha:~/python/scripts$


O comando print pode usar certas especificações para a exibição do texto. Após o texto a ser exibido com as referidas especificações deve vir um sinal de porcentagem ( % ) e uma tupla contendo as variáveis a serem substituídas pelas especificações na saída. Estas especificações podem ser %s para strings ou %d para inteiros. A tupla deve conter os itens a serem substituídos por estas especificações na mesma ordem.

Observe no primeiro uso, temos %s primeiro e este corresponde a nome que é o primeiro item da tupla, depois temos %d que corresponde a idade, que é o segundo item da tupla.

O que o Python faz aqui é converter cada item da tupla em uma string e substituir a especificação por esta string. Assim %s é substituído pelo valor da variável nome e %d é substituído pelo valor da variável idade.

Este uso do comando print facilita muito exibir os dados e evita muita manipulação de strings para conseguir o mesmo efeito. Esta técnica também evita o uso demasiado de vírgulas e torna o código mais legível.

A maioria das vezes você pode usar apenas a especificação %s , até mesmo para exibir números, e deixar o Python preocupar-se com o resto para você. Porém, você pode querer usar as especificações corretas para cada tipo de dado pois isto auxilia na detecção de erros:

>>> nome = 'samuel'
>>> idade = 38
>>> peso = 98.5
>>> print 'Meu nome é %s. Minha idade é %d. Meu peso é %.2f'%(nome,idade,peso)
Meu nome é samuel. Minha idade é 38. Meu peso é 98.50
>>>
>>> # agora vamos exibir usando só o especificador %s
... print 'Meu nome é %s. Minha idade é %s. Meu peso é %s'%(nome,idade,peso)
Meu nome é samuel. Minha idade é 38. Meu peso é 98.5
>>>
>>> # agora veja que usar o especificador correto ajuda a detectar erros
... print 'Meu nome é %s. Minha idade é %d. Meu peso é %.2f'%(nome,nome,peso)
Traceback (most recent call last):
File "<stdin>", line 2, in ?
TypeError: int argument required
>>>


Os especificadores básicos são:

%s para strings;
%d para inteiros e
%f para números reais, ou de ponto flutuante.

Por padrão o Python exibe números de ponto flutuante (reais) com cinco dígitos após a vírgula. Para alterar isto use a notação %.nf, onde n é o número de dígitos desejados após a vírgula.

>>> print 'Meu peso é %f'%(peso)
Meu peso é 98.500000
>>> print 'Meu peso é %.2f'%(peso)
Meu peso é 98.50
>>> print 'Meu peso é %.3f'%(peso)
Meu peso é 98.500
>>> print 'Meu peso é %.4f'%(peso)
Meu peso é 98.5000
>>> print 'Meu peso é %.5f'%(peso)
Meu peso é 98.50000
>>> print 'Meu peso é %.8f'%(peso)
Meu peso é 98.50000000
>>>


No segundo uso de tuplas com strings mostrado mais acima, usamos apenas um especificador %s e um item isolado sem estar em nenhuma tupla. Isto é permitido apenas para uma única especificação e um item isolado.

Dicionários

Um dicionário é como um livro de endereços onde você pode encontrar o endereço de uma pessoa apenas sabendo seu nome, ou seja, nós associamos chaves (nome) com valores (endereço). Observe que a chave deve ser única, pois caso existam duas chaves iguais (duas pessoas com o mesmo nome) você pode encontrar informações incorretas.

Você só pode usar objetos imutáveis (como strings) como chaves de um dicionário, mas para os valores você pode usar objetos mutáveis ou imutáveis. Isto basicamente significa dizer que você só deve usar objetos simples como chaves.

Pares de chaves e valores são especificados em um dicionário usando a notação

d = {chave1:valor1, chave2:valor2}

Observe que os pares chave/valor são separados por vírgula. Dentro de cada par a chave é separada do valor por dois pontos e todo o dicionário deve estar envolvido com o sinal de chaves { }.

Lembre-se que os pares chave/valor em um dicionário não são organizados por padrão. Assim, se você quiser os dados organizados em uma ordem particular, terá que organizá-los.

Os dicionários são instâncias/objetos da classe dict.

Usando dicionários

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando dicionários

# ab é a abreviatura de 'a'ddress 'b'ook

ab = {          'Swaroop' : 'swaroopch@byteofpython.info',
                'Larry' : 'larry@wall.org',
                'Matsumoto' : 'matz@ruby-lang.org',
                'Spammer' : 'spammer@hotmail.com'
         }

print "O email de Swaroop é %s" % ab['Swaroop']

# Adicionando um novo par chave/valor
ab['Guido'] = 'guido@python.org'

# Deletando par chave/valor
del ab['Spammer']

print '\nExistem %d contatos no livro de endereços\n' % len(ab)

for nome, email in ab.items():
   print 'O email de %s é %s' % (nome, email)

if 'Guido' in ab: # OU ab.has_key('Guido')
   print "\nO email de Guido é %s" % ab['Guido']


Execução:

samuel@aranha:~/python/scripts$ python dicionario.py
O email de Swaroop é swaroopch@byteofpython.info

Existem 4 contatos no livro de endereços

O email de Swaroop é swaroopch@byteofpython.info
O email de Matsumoto é matz@ruby-lang.org
O email de Larry é larry@wall.org
O email de Guido é guido@python.org

O email de Guido é guido@python.org
samuel@aranha:~/python/scripts$


Criamos o dicionário ab usando a notação citada acima. Então acessamos os pares chave/valor especificando a chave através do uso de índices semelhante ao que fizemos com as listas e tuplas. Observe que aqui com os dicionários, a sintaxe também é muito simples.

Podemos adicionar um novo par chave/valor simplesmente especificando uma nova chave e atribuindo a ela um novo valor como fizemos para Guido no exemplo acima.

Podemos apagar um par chave/valor usando o já conhecido comando del. Simplesmente especificamos o dicionário e a chave do par a ser removido e passamos para o comando del. Não há necessidade de saber o valor correspondente a chave para esta operação.

Depois acessamos cada par chave/valor do dicionário usando o método items do dicionário o qual retorna uma lista de tuplas onde cada tupla contém um par de itens, a chave seguida pelo valor. Nós recuperamos estes pares e atribuímos eles as variáveis nome e email correspondentes a cada par usando um laço for.....in e imprimimos estes valores no bloco for.

Podemos checar se um par chave/valor existe usando o operador in ou o método has_key da classe dict. Você pode ver a lista completa dos métodos da classe dict usando help(dict).

Argumentos palavra-chave e dicionários. Se você já utilizou funções com argumentos palavra-chave, então você já usou dicionários. Apenas pense assim: o par chave/valor é especificado por você na lista de parâmetros da definição da função e, quando você acessa esta variável dentro da função, está acessando através da chave de um dicionário (que é chamado tabela de símbolos na terminologia de projetos de compiladores).

Seqüências

Listas, tuplas e strings são exemplos de seqüências, mas o que são seqüências e o que há de tão especial com elas? Dois dos principais recursos de uma seqüência são o operador de índices que nos permite recuperar um determinado item numa seqüência e a capacidade de dividir a seqüência em partes menores.

Usando seqüências

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# usando seqüências

shoplist = ['apple', 'mango', 'carrot', 'banana']

# Operação de indexação
print 'Item 0 é', shoplist[0]
print 'Item 1 é', shoplist[1]
print 'Item 2 é', shoplist[2]
print 'Item 3 é', shoplist[3]
print 'Item -1 é', shoplist[-1]
print 'Item -2 é', shoplist[-2]

# Dividindo uma lista em partes menores
print 'Do item 1 ao 3 é', shoplist[1:3]
print 'Do item 2 até o fim é', shoplist[2:]
print 'Do item 1 até o -1 é', shoplist[1:-1]
print 'Do primeiro item até o último é', shoplist[:]

# Dividindo uma string em partes menores
name = 'swaroop'
print 'Do caractere 1 até o 3 é', name[1:3]
print 'Do caractere 2 até o fim é', name[2:]
print 'Do caractere 1 até o -1 é', name[1:-1]
print 'Do primeiro até o último caractere é', name[:]


Execução:

samuel@aranha:~/python/scripts$ python sequencia.py
Item 0 é apple
Item 1 é mango
Item 2 é carrot
Item 3 é banana
Item -1 é banana
Item -2 é carrot
Do item 1 ao 3 é ['mango', 'carrot']
Do item 2 até o fim é ['carrot', 'banana']
Do item 1 até o -1 é ['mango', 'carrot']
Do primeiro item até o último é ['apple', 'mango', 'carrot', 'banana']
Do caractere 1 até o 3 é wa
Do caractere 2 até o fim é aroop
Do caractere 1 até o -1 é waroo
Do primeiro até o último caractere é swaroop
samuel@aranha:~/python/scripts$


Primeiro nós vimos como usar índices para recuperar itens de uma seqüência. Sempre que você especificar um número para uma seqüência dentro de colchetes como mostrado acima, o Python buscará para você o item correspondente aquela posição na seqüência. Lembre-se que o Python inicia a contagem a partir de zero. Então shoplist[0] encontra o primeiro item e shoplist[3] encontra o quarto item da seqüência shoplist.

O índice também pode ser um número negativo. Neste caso a posição é calculada a partir do final da seqüência. Então shoplist[-1] refere-se ao último item da seqüência e shoplist[-2] encontra o penúltimo item da seqüência.

A sintaxe para dividir uma seqüência é: o nome da seqüência seguido por um par de números (opcional) separados por dois pontos e entre colchetes. Observe que isto é muito similar a operação de indexação usada até agora para recuperar itens. Lembre-se que os números são opcionais mas os dois pontos não.

O primeiro número (antes dos dois pontos) indica a posição onde a subseqüência inicia e o segundo número (após os dois pontos) indica a posição onde a subseqüência termina. Se o primeiro número não for especificado, Python assumirá que o início da subseqüência é o início da seqüência. Se o segundo número não for especificado, Python assumirá que o fim da subseqüência é o fim da seqüência. Observe que a subseqüência inicia exatamente na primeira posição (primeiro número) e termina uma unidade antes da segunda posição (antes do segundo número), ou seja a posição de início é incluída na subseqüência mas a posição de término é excluída da subseqüência.

Então, shoplist[1:3] retorna uma subseqüência que inicia na posição 1 (inclusive), passa pela posição 2 e termina na posição 3 (exclusive). Assim esta subseqüência tem dois elementos. shoplist[:] retorna toda a seqüência.

Você também pode recuperar subseqüências usando índices negativos. Números negativos são usados para posições a partir do fim da seqüência. Por exemplo, shoplist[:-1] retornará uma subseqüência que exclui o último item da seqüência mas inclui todos os outros itens.

Tente várias combinações para recuperar subseqüências usando o interpretador Python interativamente pois assim você pode ver o resultado imediatamente. A grande vantagem das seqüências é que você pode acessar todas elas (tuplas, listas e strings) com a mesma sintaxe.

Referências

Quando você cria um objeto e atribui ele a uma variável, a variável apenas refere-se ao objeto e não representa o objeto propriamente dito! Isto é, o nome da variável aponta para o local da memória do computador onde o objeto está armazenado.

Normalmente você não precisa preocupar-se com isto, mas existe uma conseqüência desta referência que você tem que tomar conhecimento. Ela é demonstrada no exemplo seguinte:

Objetos e referências

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# observando as referências aos objetos

print 'Simples atribuição'
shoplist = ['apple', 'mango', 'carrot', 'banana']
mylist = shoplist # mylist é apenas outro nome apontando para o mesmo objeto!

del shoplist[0] # Comprei o primeiro item, então este foi removido da lista

print 'shoplist é', shoplist
print 'mylist é', mylist
# observe que ambos os objetos (shoplist e mylist) imprimem a mesma lista sem
# o item 'apple', confirmando que eles apontam para o mesmo objeto

print 'Copiando o objeto'
mylist = shoplist[:] # faz uma cópia do objeto
del mylist[0] # remove o primeiro item

print 'shoplist é', shoplist
print 'mylist é', mylist
# observe que agora as duas listas são diferentes


Execução:

samuel@aranha:~/python/scripts$ python referencia.py
Simples atribuição
shoplist é ['mango', 'carrot', 'banana']
mylist é ['mango', 'carrot', 'banana']
Copiando o objeto
shoplist é ['mango', 'carrot', 'banana']
mylist é ['carrot', 'banana']
samuel@aranha:~/python/scripts$


A maioria da explanação está disponível nos comentários. O que você precisa lembrar-se é que, se você quer fazer uma cópia de uma lista ou qualquer outra seqüência ou objeto complexo (não simples objetos como números inteiros), então você tem que usar uma operação semelhante a usada neste exemplo ( mylist = shoplist[:] ) . Se você apenas atribuir outro nome a variável, as duas variáveis estarão referindo-se ao mesmo objeto e isto pode causar muitos problemas.

Mais sobre strings

Já discutimos antes sobre strings e você já sabe que strings são objetos e que tem métodos. As strings pertencem a classe str. O exemplo abaixo demonstra alguns métodos úteis da classe str. Para ver uma lista completa dos métodos veja help(str):

Métodos das strings

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# alguns métodos das strings

name = 'Swaroop' # Este é um objeto string

if name.startswith('Swa'):
   print 'Sim, a strings inicia com "Swa"'

if 'a' in name:
   print 'Sim, ela contém a string "a"'

if name.find('war') != -1:
   print 'Sim, ela contém a string "war"'

delimiter = '_*_'
mylist = ['Brazil', 'Russia', 'India', 'China']
print delimiter.join(mylist)


Execução:

samuel@aranha:~/python/scripts$ python metodos_strings.py
Sim, a strings inicia com "Swa"
Sim, ela contém a string "a"
Sim, ela contém a string "war"
Brazil_*_Russia_*_India_*_China
samuel@aranha:~/python/scripts$


Aqui nós vemos vários métodos das strings em ação. O método starwidth é usado para verificar se a string inicia com uma dada substring. O operador in é usado para checar se uma dada substring faz parte da string.

O método find é usado para encontrar a posição de uma substring numa string. Caso não encontre a posição (a substring não faz parte da string) ele retorna -1.

O método join é usado para juntar os itens de uma seqüência com uma string como separador.