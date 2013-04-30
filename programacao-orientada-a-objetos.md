Programação orientada a objetos

Introdução

Até agora projetamos nossos programas em torno de funções ou blocos de comandos que manipulam dados. Isto é chamado programação orientada a função. Existe outra maneira de organizar seu programa que é combinar dados e funcionalidade e colocar tudo dentro do que é chamado de objeto. Isto é chamado programação orientada a objetos. A maioria das vezes você pode usar programação orientada a função, mas algumas vezes, quando você quer escrever grandes programas ou quando oferece uma solução melhor, você pode usar a orientação a objetos.

Classes e objetos são as duas principais características da programação orientada a objetos. Uma classe cria um novo tipo onde objetos são instâncias da classe. Uma analogia é que você pode ter variáveis do tipo int, o que significa que variáveis que armazenam valores inteiros são instâncias (objetos) da classe int.

Objetos podem armazenar dados usando variáveis comuns que pertencem ao objeto. Variáveis que pertencem a um objeto ou classe são chamadas de campos. Objetos também podem ter funcionalidade através da utilização de funções que pertencem a uma classe. Estas funções são chamadas de métodos da classe. Esta terminologia é importante pois nos ajuda a diferenciar as funções e variáveis comuns daquelas que pertencem a uma classe ou objeto. Os campos e métodos podem ser referenciados como sendo os atributos de uma classe.

Campos podem ser de dois tipos, eles podem pertencer a cada instância/objeto da classe ou pertencer a classe propriamente dita. São chamados respectivamente variáveis de instância e variáveis de classe.

Uma classe é criada usando a palavra-chave class. Os campos e métodos da classe são listados em um bloco de comandos indentado.

self

Os métodos de uma classe tem apenas uma diferença das funções normais. Eles devem ter um primeiro nome extra que deve ser adicionado ao início da lista de parâmetros, mas você não deve atribuir valor a este parâmetro quando chamar o método, Python fará isto. Esta variável especial refere-se ao próprio objeto e por convenção é chamada self.

Embora você possa atribuir qualquer nome a este parâmetro é altamente recomendável que você use o nome self. Existem muitas vantagens em usar o nome padrão. Qualquer um que ler seu programa imediatamente entenderá e até mesmo as ferramentas IDE (ambientes de desenvolvimento gráfico) lhe ajudarão se você usar o nome self.

Você deve estar maravilhado sobre como Python atribui um valor a self e sobre porque você mesmo não precisa fazer isto. Um exemplo tornará isto mais claro. Digamos que você tem uma classe chamada MinhaClasse e uma instância desta classe chamada MeuObjeto. Quando você chama um método deste objeto como MeuObjeto.método(arg1, arg2), isto é automaticamente convertido por Python para MinhaClasse.método(MeuObjeto, arg1, arg2). É isto que self proporciona.

Isto também significa que, mesmo que você tem um método que não recebe nenhum argumento, ainda assim você deve definir que este tenha o argumento self.

Classes

A classe mais simples possível é mostrada no exemplo seguinte:

Criando uma classe

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# classe.py

class Person:
  pass # Um bloco de comandos vazio

p = Person()
print p


Execução:

samuel@aranha:~/python/scripts$ python classe.py
<__main__.Person instance at 0x401e022c>
samuel@aranha:~/python/scripts$


Criamos uma nova classe com o comando class seguido do nome da nova classe. Depois disto segue um bloco de comandos que constitui o corpo da classe. Neste caso temos um bloco de comandos vazio, o qual é indicado pelo comando pass.

Depois criamos um objeto/instância desta classe usando o nome da classe seguido de parênteses. Para verificação, exibimos a variável criada com o comando print.

Ao executarmos o programa, vemos que a saída nos exibe que a variável é uma instância da classe Person no módulo __main__.

Observe que o endereço de memória onde a variável está armazenada também é exibido. Provavelmente este endereço seja diferente do mostrado no seu computador pois Python pode armazenar a variável em qualquer lugar disponível na memória.

Métodos

Como já dito antes, classes/objetos podem ter métodos que nada mais são que funções. A diferença entre funções normais e métodos é que estes possuem uma variável extra chamada self. Exemplo do uso de métodos:

Usando métodos

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# metodo.py

class Person:
  def alo(self):
    print 'Alô Mundo!!!'

p = Person()

p.alo()

print 'chamando com outra sintaxe'

Person().alo()


Execução:

samuel@aranha:~/python/scripts$ python metodo.py
Alô Mundo!!!
chamando com outra sintaxe
Alô Mundo!!!
samuel@aranha:~/python/scripts$


Aqui nós vemos self em ação. Observe que o método Alo não tem nenhum parâmetro, mas mesmo assim possui self em sua definição.

__init__

Existem vários métodos especiais em Python, __init__ é um deles. __init__ é chamado quando um objeto de uma classe é instânciado. Este método é útil para fazer qualquer inicialização que você queira com seu objeto. Observe os dois sinais de sublinhado no início e no final do nome.

Usando o método __init__

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# init.py

class Person:
  def __init__(self,nome):
    self.nome = nome
  def alo(self):
    print 'Alô, meu nome é',self.nome

p = Person('Samuel')

p.alo()

print 'chamando com outra sintaxe'

Person('Samuel').alo()


Execução:

samuel@aranha:~/python/scripts$ python init.py
Alô, meu nome é Samuel
chamando com outra sintaxe
Alô, meu nome é Samuel
samuel@aranha:~/python/scripts$


Aqui nós definimos o método __init__ pegando um parâmetro chamado nome além do usual self. Criamos um novo campo, também chamado nome. Observe que apesar de terem os mesmos nomes estas são variáveis diferentes. A sintaxe utilizando o ponto nos permite diferenciá-las.

O mais importante é observar que não chamamos __init__ diretamente, passamos os argumentos dentro dos parênteses que seguem o nome da classe quando criamos uma nova instância dela. Isto é o significado especial deste método.

Agora podemos usar o campo self.nome em nossos métodos como demonstrado no método alo do exemplo.

Variáveis de objetos e classes

Já discutimos a funcionalidade das classes e objetos, agora veremos como as classes e os objetos armazenam dados. Atualmente estes dados nada mais são que variáveis comuns que estão limitadas ao espaço de nome das classes e objetos, isto é, seus nomes só são válidos no contexto destas classes e objetos.

Existem dois tipos de campos, variáveis de classe e variáveis de objeto, dependendo de quem a variável pertence.

Variáveis de classe são acessadas por todos objetos (instâncias) da classe. Existe apenas uma cópia da variável de classe e quando um objeto altera esta variável, a alteração é refletida em todas as outras instâncias da classe.

Variáveis de objeto pertencem a determinado(a) objeto/instância da classe. Neste caso cada objeto tem sua própria cópia do campo, isto é, este campo não é compartilhado nem está relacionado a um outro campo de mesmo nome que pertence a outra instância da classe. Um exemplo tornará isto mais claro.

Usando variáveis de objeto e de classe

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

class Pessoa:
  '''Representa uma pessoa.'''
  populacao = 0

  def __init__(self, nome):
    '''Inicializa os dados da pessoa.'''
    self.nome = nome
    print '(Inicializando %s)' % self.nome

    # Quando esta pessoa é criada, ele/ela
    # é adicionado a população
    Pessoa.populacao += 1

    def __del__(self):
    '''Eu estou morrendo.'''
    print 'Tchau %s.' % self.nome

        Pessoa.populacao -= 1

        if Pessoa.populacao == 0:
      print 'Eu sou o último.'
    else:
      print 'Ainda existem %d pessoas.' % Pessoa.populacao

    def Alo(self):
    '''Saudando as pessoas.

    Ralmente, isto é tudo que este método faz.'''

        print 'Oi, meu nome é %s.' % self.nome

    def censo(self):
   '''Exibe a população atual.'''

      if Pessoa.populacao == 1:
      print 'Eu sou a única pessoa aqui.'
   else:
      print 'Nós temos %d pessoas aqui.' % Pessoa.populacao

samuel = Pessoa('Samuel')
samuel.Alo()
samuel.censo()

swaroop = Pessoa('Swaroop')
swaroop.Alo()
swaroop.censo()

kalam = Pessoa('Abdul Kalam')
kalam.Alo()
kalam.censo()

samuel.Alo()
samuel.censo()

print 'Terminando de usar a classe'
print

Execução:

samuel@aranha:~/python/scripts$ python var_de_obj_e_de_classe.py
(Inicializando Samuel)
Oi, meu nome é Samuel.
Eu sou a única pessoa aqui.
(Inicializando Swaroop)
Oi, meu nome é Swaroop.
Nós temos 2 pessoas aqui.
(Inicializando Abdul Kalam)
Oi, meu nome é Abdul Kalam.
Nós temos 3 pessoas aqui.
Oi, meu nome é Samuel.
Nós temos 3 pessoas aqui.
Terminando de usar a classe

Tchau Abdul Kalam.
Ainda existem 2 pessoas.
Tchau Samuel.
Ainda existem 1 pessoas.
Tchau Swaroop.
Eu sou o último.
samuel@aranha:~/python/scripts$


Este exemplo é grande mas ajuda a demonstrar a natureza das variáveis de objetos e classes. Aqui, populacao pertence a classe Pessoa, então é uma variável de classe. A variável nome pertence ao objeto (ela é atribuída usando self) e então é uma variável de objeto.

Assim, nos referimos a variável de classe populacao como Pessoa.populacao e não como self.populacao. Observe que uma variável de objeto com o mesmo nome de uma variável de classe esconderá a variável de classe! Nos métodos do objeto, nós nos referimos a variável de objeto nome usando a notação self.nome. Lembre-se destas simples diferenças entre as variáveis de objeto e as variáveis de classe.

Observe que o método __init__ é usado para inicializar uma instância de Pessoa com um nome. Neste método nós incrementamos a população de uma unidade, uma vez que uma pessoa está sendo adicionada.

Lembre-se que você deve referir-se a variáveis e métodos do mesmo objeto usando apenas a variável self. Isto é chamado atribuição por referência.

Neste programa, também vemos o uso de docstrings tanto nas classes quanto nos métodos. Podemos acessar a docstring da classe, em tempo de execução, usando Pessoa.__doc__ e a docstring do método usando Pessoa.Alo.__doc__

Como __init__ existe outro método especial __del__ o qual é chamado quando o objeto está sendo encerrado, isto é, ele não está mais sendo usado. Neste método nós apenas decrementamos Pessoa.populacao de uma unidade.

O método __del__ é executado quando o objeto não está mais em uso e não há garantia de quando ele será executado. Se você quer explicitamente fazer isto, deve usar o comando del visto nos exemplos anteriores.

Herança

Um dos maiores benefícios da programação orientada a objetos é reutilizar o código e uma das maneiras de fazer isto é através do mecanismo de herança. A herança pode ser melhor imaginada como a implementação de um relacionamento tipo e subtipo entre classes.

Suponha que você quer escrever um programa para processar os dados de professores e estudantes em uma escola. Eles tem algumas características comuns como nome, idade e endereço. Eles também tem características específicas como salário, cursos e licenças para professores e notas e mensalidades para estudantes.

Você pode criar uma classe diferente para cada tipo, porém adicionar uma nova característica comum significa adicionar esta característica nas duas classes. Isto rapidamente torna-se incomodo.

Uma melhor maneira seria criar uma classe comum chamada MembroDaEscola e ter as classes Professor e Estudante herdando dela, isto é, Professor e Estudante seriam subtipos de MembroDaEscola, que seria o tipo. Então deveríamos adicionar as características específicas aos subtipos.

Existem várias vantagens nesta abordagem. Se nós adicionamos/alteramos qualquer funcionalidade em MembroDaEscola, isto é automaticamente refletido nos subtipos. Por exemplo, você pode adicionar um número de identificação NR para professores e estudantes simplesmente adicionando isto a classe MembroDaEscola. Porém, alterações nos subtipos não alteram outros subtipos. Outra vantagem é que você pode referir-se a um objeto professor ou estudante como um objeto MembroDaEscola, o que pode ser útil em algumas situações, como numa contagem do número de membros da escola. Isto é chamado poliformismo, onde um subtipo pode ser substituído em qualquer situação onde um tipo é esperado, isto é, o objeto pode ser tratado como uma instância da classe pai.

Observe também que nós reutilizamos o código da classe pai não precisando repetí-lo em diferentes classes, como fizemos no caso das classes independentes.

A classe MembroDaEscola nesta situação é conhecida como classe base ou superclasse. Professor e Estudante são chamadas classes derivadas ou subclasses.

Agora veremos um exemplo:

Usando herança

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

class MembroDaEscola:
  '''Representa qualquer membro da escola.'''
  def __init__(self, nome, idade):
    self.nome = nome
    self.idade = idade
    print '(Inicializando membro: %s)' % self.nome

  def exibe(self):
  '''Exibe meus detalhes.'''
  print 'Nome:"%s" Idade:"%s"' % (self.nome, self.idade),

class Professor(MembroDaEscola):
  '''Representa um professor.'''

  def __init__(self, nome, idade, salario):
    MembroDaEscola.__init__(self, nome, idade)
    self.salario = salario
    print '(Inicializando Profesor: %s)' % self.nome

  def exibe(self):
    MembroDaEscola.exibe(self)
    print 'Salário: "%d"' % self.salario

class Estudante(MembroDaEscola):
 '''Representa um estudante.'''

  def __init__(self, nome, idade, nota):
    MembroDaEscola.__init__(self, nome, idade)
    self.nota = nota
    print '(Inicializando Estudante: %s)' % self.nome

  def exibe(self):
    MembroDaEscola.exibe(self)
    print 'Nota: "%d"' % self.nota

p = Professor('Mr. Swaroop', 22, 30000)
e = Estudante('Samuel', 38, 75)

print # imprime uma linha em branco

membros = [p, e]
for membro in membros:
  membro.exibe() # trabalha para ambos: Professores e Estudantes


Execução:

samuel@aranha:~/python/scripts$ python heranca.py
(Inicializando membro: Mr. Swaroop)
(Inicializando Profesor: Mr. Swaroop)
(Inicializando membro: Samuel)
(Inicializando Estudante: Samuel)

Nome:"Mr. Swaroop" Idade:"22" Salário: "30000"
Nome:"Samuel" Idade:"38" Nota: "75"
samuel@aranha:~/python/scripts$


Para usar a herança nós colocamos, na definição da classe derivada, uma tupla com os nomes das classes base logo após o nome da classe derivada. Depois nós vemos que o método __init__ da classe base é explicitamente chamado usando a variável self, assim podemos inicializar a parte da classe base do objeto. É muito importante lembrar disto, Python não chama o construtor da classe base automaticamente, você tem que fazer isto explicitamente.

Também observamos que podemos chamar métodos da classe base apenas colocando o nome da classe antes da chamada do método e passando a variável sem self argumentos.

Note que podemos tratar instâncias de Professor e Estudante como instâncias de MembroDaEscola quando usamos o método exibe da classe MembroDaEscola.

Observe também que ao chamarmos o método exibe no laço for, é o do subtipo que é chamado e não o da classe MembroDaEscola. Isto porque Python sempre procura por um método no tipo atual e, se não o encontra, aí sim é que procura nas classes bases que foram especificadas na tupla da definição, na ordem em que foram especificadas.

Quando mais de uma classe é citada na tupla da herança, isto é chamado múltipla herança.