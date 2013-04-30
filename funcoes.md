Funções

Funções são pequenos trechos de código reutilizáveis. Elas permitem dar um nome a um bloco de comandos e rodar este bloco usando o nome, a partir de qualquer lugar do programa, quantas vezes você quiser. Isto é conhecido como “chamar” a função. Nós já usamos algumas funções internas do Python como len e range.

Definição

Funções são definidas usando a palavra-chave def. Esta é seguida pelo nome da função, um par de parênteses que pode envolver algumas variáveis, dois pontos e o bloco de comandos:

Definindo uma função

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# utilizando funções

# Definindo a função alo()
def alo():
  print 'Alô Mundo'


# Chamando a função alo()
alo()


Execução:

samuel@aranha:~/python/scripts$ python funcao1.py
Alô Mundo
samuel@aranha:~/python/scripts$

Parâmetros e argumentos

Nossa função alo() foi definida de acordo com a sintaxe descrita acima. Ela porém, não possui nenhum parâmetro. Parâmetros são as variáveis que podem ser incluídas nos parênteses da definição. O bloco de comandos da função pode utilizar estas variáveis para processar a informação e executar algum trabalho útil. Quando a função é chamada são passados valores a serem atribuídos a estas variáveis, estes valores são chamados argumentos.

Abaixo temos um exemplo de uma função que possui parâmetros em sua definição e por sua vez exige argumentos na chamada:

Usando parâmetros e argumentos numa função

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# utilizando funções com parâmetros e argumentos

def soma(a,b): # a e b são os parâmetros da função 
  print 'A soma de',a,'e',b,'é',a + b

# Chamando a função soma()

soma(3,4) # 3 e 4 são os argumentos da função


Execução:

samuel@aranha:~/python/scripts$ python funcao2.py
A soma de 3 e 4 é 7
samuel@aranha:~/python/scripts$


Outro exemplo:

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

def maior_nr(a,b):
  if a > b:
    print a,'é maior que',b
  else:
    print b,'é maior que',a

maior_nr(5,7)

x = 13
y = 9

maior_nr(x,y)


Execução:

samuel@aranha:~/python/scripts$ python funcao3.py
7 é maior que 5
13 é maior que 9
samuel@aranha:~/python/scripts$


Observe que tanto podemos chamar a função com argumentos numéricos como em maior_nr(5,7), quanto podemos chamá-la passando variáveis como argumento como em maior_nr(x,y). Quando chamados maior_nr(x,y), o valor de x foi atribuído ao parâmetro a e o valor de y foi a atribuído ao parâmetro b.

Variáveis locais

Quando você declara uma variável dentro de uma função, ela é totalmente independente de qualquer outra variável que tenha o mesmo nome fora da função, isto é, nomes de variáveis são locais a função. Isto é chamado escopo da variável. Todas as variáveis tem o escopo do bloco de comandos em que foram criadas. O exemplo abaixo demonstra isto:

Usando variáveis locais

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# verificando que variáveis tem escopo local

def func(x):
  print 'x é', x
  x = 2
  print 'Valor local de x alterado para', x

x = 50
func(x)
print 'x ainda é', x


Execução:

samuel@aranha:~/python/scripts$ python escopo_local.py
x é 50
Valor local de x alterado para 2
x ainda é 50
samuel@aranha:~/python/scripts$


Na função, quando usamos o valor de x pela primeira vez, o Python usa o valor passado como argumento, no caso 50.

Depois atribuímos o valor 2 a x. O nome x é local a nossa função. Assim, quando alteramos o valor de x na função o x definido no bloco principal permanece inalterado. A última instrução print confirma isto.

Variáveis globais

Se você quiser atribuir um valor a uma variável definida fora da função você terá informar ao Python que a variável não é local, mas sim global. Nós fazemos isto usando a instrução global. É impossível atribuir um valor a uma variável fora da função sem utilizar a instrução global.

Você pode usar o valor de variáveis definidas fora da função (considerando que não existem variáveis com o mesmo nome dentro da função). Porém isto é desencorajado e deve ser evitado uma vez que torna-se difícil para o leitor saber onde a definição da variável está. Usar a instrução global torna claro que a variável foi definida fora da função.

Usando variáveis globais

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

def func():
  global x
  print 'x é', x
  x = 2
  print 'Valor de x (que é global) alterado para', x

x = 50
func()
print 'O valor de x é', x


Execução:

samuel@aranha:~/python/scripts$ python global.py
x é 50
Valor de x (que é global) alterado para 2
O valor de x é 2


A instrução global é usada para declarar x como uma variável global. Assim, quando atribuímos uma valor a x dentro da função a alteração é refletida quando utilizamos o valor de x no bloco principal.

Você pode especificar mais de uma variável global usando o mesmo comando. Por exemplo: global x, y, z.

Valores padrão para argumentos

Ao definir funções, você pode querer que alguns parâmetros sejam opcionais. Assim, o usuário pode usar valores padrão previamente definidos caso não queira entrar com os referidos parâmetros. Isto é feito com a ajuda dos valores padrão para argumentos. Você pode especificar um valor padrão para um argumento seguindo o nome dele com o operador de atribuição ( = ) e depois com o referido valor padrão.

Observe que o valor padrão do argumento deve ser uma constante. Mais precisamente, o valor padrão de um argumento deve ser imutável – isto será explicado em detalhes mais a frente. Por enquanto, apenas lembre disto.

Usando valores padrão de argumentos

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# função que usa valores padrão para argumentos

def exibe_msg(mensagem, vezes = 1):
  print mensagem * vezes


exibe_msg('Alo...câmbio')
exibe_msg('Python', 5)


Execução:

samuel@aranha:~/python/scripts$ python funcao4.py
Alo...câmbio
PythonPythonPythonPythonPython
samuel@aranha:~/python/scripts$


A função exibe_msg() é usada para exibir uma string várias vezes. Se o número de vezes não é fornecido, o valor padrão é usado e a string é exibida apenas uma vez. Isto é feito pela atribuição do valor padrão 1 para o argumento vezes.

No primeiro uso, nós não fornecemos o segundo argumento e a mensagem foi exibida apenas uma vez de acordo com o valor padrão. No segundo uso passamos dois argumentos, a string a ser exibida e o número de vezes que esta deve ser exibida.

IMPORTANTE: os parâmetros que terão valores padrão devem estar no fim da lista de parâmetros, isto é você não pode ter um parâmetro com valor padrão antes de um que não tenha na lista de parâmetros da definição da função.

Isto porque os valores são atribuídos aos parâmetros pela posição. Por exemplo def func(a, b=5) é válido mas, def func(a=5, b) não é válido.

Argumento palavra-chave

Se sua função tem muitos parâmetros e você quer especificar apenas alguns deles, você pode atribuir valores aos parâmetros nomeando-os. Isto é chamado argumento palavra-chave. Nós usamos um nome (palavra-chave) em vez da posição para especificar os argumentos na função.

Esta técnica traz duas vantagens. Primeiro que usar a função é mais fácil, uma vez que você não precisa preocupar-se com a ordem dos argumentos. Segundo que podemos atribuir valores apenas aos parâmetros que quisermos contanto que os outros parâmetros tenham valores padrão.

Usando argumentos palavra-chave

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# função que usa argumento palavra-chave

def func(a, b=5, c=10):
  print 'a vale', a, ', b vale', b, 'e c vale', c

func(3, 7)
func(25, c=24)
func(c=50, a=100)


Execução:

samuel@aranha:~/python/scripts$ python funcao5.py
a vale 3 , b vale 7 e c vale 10
a vale 25 , b vale 5 e c vale 24
a vale 100 , b vale 5 e c vale 50
samuel@aranha:~/python/scripts$


A função tem um parâmetro sem valor padrão (a) seguida de dois com valor padrão definido (b e c).

No primeiro uso, func(3,7), o parâmetro a ganha o valor de 3, o parâmetro b ganha o valor de 7 e o parâmetro c mantém o valor padrão de 10.

No segundo uso, func(25, c=24), o parâmetro a ganha o valor de 25 devido a posição do argumento. Então, o parâmetro c ganha o valor de 24 devido ao seu uso nomeado, ou seja usando a técnica da palavra-chave. O parâmetro b ganha seu valor padrão de 5.

No terceiro uso, func(c=50, a=100), nós só usamos palavras-chave para especificar os argumentos. Observe que especificamos o valor do parâmetro c antes do valor do parâmetro a, embora a esteja antes de c na definição da função.

return

O comando return é usado para retornar da função, isto é, encerrá-la. Opcionalmente podemos retornar um valor ao encerrar a função.

Usando o comando return

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# função que retorna um valor

def maior(x, y):
  if x > y:
    return x
  else:
    return y

print maior(2, 3)


Execução:

samuel@aranha:~/python/scripts$ python return.py
3
samuel@aranha:~/python/scripts$


A função maior() retorna o maior entre os dois valores, no caso os números fornecidos como argumento. Ela usa um simples comando if...else para encontrar o maior valor e então retorna este.

Observe que o comando return sem um valor equivale a return None. None é um tipo especial em Python que significa nada, sem valor. Por exemplo, se uma variável recebeu o valor None, isto significa que ela não tem valor.

Toda função implicitamente tem um comando return None no final a menos que você tenha escrito seu próprio comando return. Você pode ver isto rodando print func() onde a função func() não usa return, como em:

>>> def func():
... pass
...
>>> print func()
None
>>> samuel@aranha:~/python/scripts$

O comando pass é usado para indicar um bloco de comandos vazio.

Docstrings

Python tem um recurso chamado documentation strings que normalmente é referenciado pela abreviatura docstring. Docstring é uma importante ferramenta que você deve usar uma vez que ela ajuda a documentar melhor seu programa tornando-o mais fácil de ser entendido. Nós podemos até mesmo exibir a docstring definida na função enquanto nosso programa está rodando.

Usando docstrings

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

# função com docstring

def exibe_maior(x, y):
  '''Exibe o maior entre dois números.
  Os dois números devem ser inteiros.'''

  x = int(x) # converte para inteiro, se possível
  y = int(y)

  if x > y:
    print x, 'é maior'
  else:
    print y, 'é maior'

exibe_maior(3, 5)
print exibe_maior.__doc__


Execução:

samuel@aranha:~/python/scripts$ python docstring.py
5 é maior
Exibe o maior entre dois números.

Os dois números devem ser inteiros.
samuel@aranha:~/python/scripts$


A string colocada no início da função é a docstring de nossa função. Observe que docstring também se aplica a módulos e classes. Aprenderemos sobre estes dois nos capítulos a frente.

Existe uma convenção que deve ser seguida ao fazer uma docstring. A primeira linha tem uma explicação rápida do que faz a função, esta deve iniciar com letra maiúscula e terminar com um ponto. A segunda linha deve ser pulada, ou seja, em branco. A explanação detalhada e/ou observações sobre o uso da função deve estar a partir da terceira linha. Você SEMPRE deve seguir estas convenções ao criar suas docstrings.

Nós acessamos a docstring de exibe_maior() através do atributo __doc__ da função (observe os dois sublinhados no início e no final). Apenas lembre que Python trata tudo como objeto inclusive as funções. Aprenderemos mais sobre objetos no capítulo classes.

Se você já usou a função help() do python, então você já viu a utilidade das docstrings. O que help() faz é apenas exibir para você a docstring do objeto passado como argumento. Você pode fazer isto com a função acima, basta incluir help(exibe_maior) em seu programa. Lembre-se de pressionar q para sair do help.

Outras ferramentas podem recuperar a documentação do seu programa desta mesma maneira. Por exemplo, o comando pydoc trabalha de maneira semelhante a help(). Assim, é altamente recomendável que você use docstrings.