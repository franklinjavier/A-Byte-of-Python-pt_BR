# Primeiros passos

Existem duas maneiras de utilizar Python: usar o modo interativo digitando comandos diretamente no interpretador ou escrever os comandos num arquivo fonte e depois executar este arquivo.

## Usando o interpretador

Para iniciar o interpretador basta digitar o comando python no shell:

**Usando o interpretador Python**

```python
samuel@aranha:~$ python
Python 2.3.5 (#2, Sep 4 2005, 22:01:42)
[GCC 3.3.5 (Debian 1:3.3.5-13)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```


O interpretador está pronto para receber comandos. O sinal >>> é o prompt primário.

Agora digite o comando print ' Alô Mundo!' e pressione ENTER:

samuel@aranha:~$ python
Python 2.3.5 (#2, Sep 4 2005, 22:01:42)
[GCC 3.3.5 (Debian 1:3.3.5-13)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> print 'Alô Mundo!'
Alô Mundo!
>>>


O comando print exibe uma string na tela.
Para sair do interpretador pressione CTRL + D.

Usando um arquivo fonte

Com seu editor de textos favorito digite o código abaixo:

Usando um arquivo fonte

#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

print 'Alô Mundo!'


Salve o arquivo como alo.py.
Conceda permissão de execução a este arquivo (chmod +x alo.py) e execute-o:

samuel@aranha:~/python/scripts$ chmod +x alo.py
samuel@aranha:~/python/scripts$ ./alo.py
Alô Mundo!
samuel@aranha:~/python/scripts$


Pronto. Você criou seu primeiro programa Python.
A primeira linha do nosso programa diz que o código do nosso arquivo deverá ser executado pelo interpretador Python.
A segunda linha diz a codificação que iremos usar. Sempre insira esta linha para usar caracteres do nosso idioma como ç, ã, é, etc...

Ajuda do Python

Se você quiser usar a ajuda do Python basta digitar help() no interpretador. Porém ela é toda em inglês.

>>> help()

Welcome to Python 2.3! This is the online help utility.

If this is your first time using Python, you should definitely check out the tutorial on the Internet at http://www.python.org/doc/tut/.

Enter the name of any module, keyword, or topic to get help on writing Python programs and using Python modules. To quit this help utility and return to the interpreter, just type "quit".

To get a list of available modules, keywords, or topics, type "modules", "keywords", or "topics". Each module also comes with a one-line summary of what it does; to list the modules whose summaries contain a given word such as "spam", type "modules spam".

help>