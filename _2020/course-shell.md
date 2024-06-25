---
layout: lecture
title: "Visão Geral do Curso + o shell"
date: 2020-01-13
ready: true
video:
  aspect: 56.25
  id: Z56Jmr9Z34Q
---

# Motivação

Como cientistas da computação, sabemos que computadores são ótimos para ajudar
em tarefas repetitivas. Contudo, com muita frequência, nós nos esquecemos que
isto se aplica tanto para nosso _uso_ do computador quanto para as computações
que nós queremos que nossos programas façam. Nós temos uma vasta coleção de
ferramentas disponíveis nas pontas dos nossos dedos que nos permitem ser mais
produtivos e resolver problemas mais complexos quando trabalhamos em qualquer
problema relacionado a computadores. Mesmo assim, muitos de nós utilizamos
apenas uma pequena fração destas ferramentas; só sabemos de cor apenas os
encantamentos mágicos suficientes para sobreviver, e cegamente copiamos e
colamos comandos da internet quando ficamos atolados.

Este curso é uma tentativa de tratar isto.

Nós queremos te ensinar como tirar o máximo das ferramentas que você conhece,
e te mostrar novas ferramentas para adicionar à sua caixa de ferramentas, e
esperançosamente incutir em você alguma empolgação para explorar (e talvez
construir) mais ferramentas por conta própria. Isto é o que nós acreditamos
ser o semestre que faltava da maioria dos currículos de Ciência da Computação.

# Estrutura do Curso

#todo: Descrever a estrutura do curso

# O Shell

## O que é o Shell?

Computadores, atualmente, possuem uma variedade de interfaces para dar
comandos; Interfaces gráficas caprichadas, interfaces de voz, e até mesmo
Realidade Virtual/Aumentada estão por toda a parte. Elas são ótimas para 80%
dos casos de uso, mas elas frequentemente são fundamentalmente restritas no
que elas te permitem fazer - você não consegue pressionar um botão que não
está lá ou dar um comando de voz que não foi programado. Pra tirar total
vantagem das ferramentas que o seu computador fornece, nós temos que partir
pra velha escola e apelar para uma interface de texto: o shell.

Quase todas as plataformas em que você puser suas mãos terão um shell de
uma forma ou outra, e muitas delas terão vários shells para você escolher.
Enquanto eles podem variar nos detalhes, em sua essência eles são todos 
grosseiramente iguais: eles permitem que você rode programas, os dê uma
entrada, e inspecione sua saída de uma maneira semi-estruturada.

Nesta aula, nós iremos focar no Bourne Again Shell, ou "bash" para abreviar.
Este é um dos shells mais amplamente usados, e sua sintaxe é similar ao que
você vai ver em muitos outros shells. Para abrir um _prompt_ do shell (onde
você pode digitar comandos), você primeiro precisa de um _terminal_. Seu 
dispositivo provavelmente possui um instalado, ou você pode facilmente
instalar um.

## Usando o Shell

Quando você abrir seu terminal, você verá um _prompt_ que normalmente parece
um pouco como isto:

```console
semestre:~$ 
```

Esta é a interface de texto principal do shell. Ela te diz que você está
na máquina "semestre", e que seu "diretório de trabalho atual", ou onde você
está neste momento, é `~` (abreviação para "home", ou o diretório inicial
do seu usuário). O `$` diz que você não é o usuário `root` (mais sobre isso
depois). Neste prompt você pode digitar um _comando_, que será então interpretado
pelo shell. O comando mais básico é executar um programa:

```console
missing:~$ date
Tue Jun 25 11:28:42 -03 2024
missing:~$ 
```

Aqui, nós executamos o programa `date`, que (talvez, pra surpresa de ninguém)
imprime a data e hora atuais. O shell então pede por outro comando pra executar.
Nós podemos também executar um comando com _argumentos_:

```console
missing:~$ echo Olá
hello
```

Neste caso, nós dissemos ao shell para executar o programa `echo` com o
argumento `Olá`. O programa `echo` simplesmente imprime seus argumentos.
O shell analisa o comando separando-o por espaços, e então roda o programa
indicado pela primeira palavra, fornecendo cada palavra subsequente como
um argumento que o programa poderá acessar. Se você fornecer um argumento
que contenha espaços ou outros caracteres especiais (ex: um diretório com
o nome "Minhas Fotos"), você pode ou indicar o argumento com `'` ou `"`
(`"Minhas Fotos"`), ou usar caracteres de escape com `\` (`Minhas\ Fotos`).

But how does the shell know how to find the `date` or `echo` programs?
Well, the shell is a programming environment, just like Python or Ruby,
and so it has variables, conditionals, loops, and functions (next
lecture!). When you run commands in your shell, you are really writing a
small bit of code that your shell interprets. If the shell is asked to
execute a command that doesn't match one of its programming keywords, it
consults an _environment variable_ called `$PATH` that lists which
directories the shell should search for programs when it is given a
command:


```console
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

When we run the `echo` command, the shell sees that it should execute
the program `echo`, and then searches through the `:`-separated list of
directories in `$PATH` for a file by that name. When it finds it, it
runs it (assuming the file is _executable_; more on that later). We can
find out which file is executed for a given program name using the
`which` program. We can also bypass `$PATH` entirely by giving the
_path_ to the file we want to execute.

## Navigating in the shell

A path on the shell is a delimited list of directories; separated by `/`
on Linux and macOS and `\` on Windows. On Linux and macOS, the path `/`
is the "root" of the file system, under which all directories and files
lie, whereas on Windows there is one root for each disk partition (e.g.,
`C:\`). We will generally assume that you are using a Linux filesystem
in this class. A path that starts with `/` is called an _absolute_ path.
Any other path is a _relative_ path. Relative paths are relative to the
current working directory, which we can see with the `pwd` command and
change with the `cd` command. In a path, `.` refers to the current
directory, and `..` to its parent directory:

```console
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ pwd
/home
missing:/home$ cd ..
missing:/$ pwd
/
missing:/$ cd ./home
missing:/home$ pwd
/home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
missing:~$ ../../bin/echo hello
hello
```

Notice that our shell prompt kept us informed about what our current
working directory was. You can configure your prompt to show you all
sorts of useful information, which we will cover in a later lecture.

In general, when we run a program, it will operate in the current
directory unless we tell it otherwise. For example, it will usually
search for files there, and create new files there if it needs to.

To see what lives in a given directory, we use the `ls` command:

```console
missing:~$ ls
missing:~$ cd ..
missing:/home$ ls
missing
missing:/home$ cd ..
missing:/$ ls
bin
boot
dev
etc
home
...
```

Unless a directory is given as its first argument, `ls` will print the
contents of the current directory. Most commands accept flags and
options (flags with values) that start with `-` to modify their
behavior. Usually, running a program with the `-h` or `--help` flag
will print some help text that tells you what flags
and options are available. For example, `ls --help` tells us:

```
  -l                         use a long listing format
```

```console
missing:~$ ls -l /home
drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing
```

This gives us a bunch more information about each file or directory
present. First, the `d` at the beginning of the line tells us that
`missing` is a directory. Then follow three groups of three characters
(`rwx`). These indicate what permissions the owner of the file
(`missing`), the owning group (`users`), and everyone else respectively
have on the relevant item. A `-` indicates that the given principal does
not have the given permission. Above, only the owner is allowed to
modify (`w`) the `missing` directory (i.e., add/remove files in it). To
enter a directory, a user must have "search" (represented by "execute":
`x`) permissions on that directory (and its parents). To list its
contents, a user must have read (`r`) permissions on that directory. For
files, the permissions are as you would expect. Notice that nearly all
the files in `/bin` have the `x` permission set for the last group,
"everyone else", so that anyone can execute those programs.

Some other handy programs to know about at this point are `mv` (to
rename/move a file), `cp` (to copy a file), and `mkdir` (to make a new
directory).

If you ever want _more_ information about a program's arguments, inputs,
outputs, or how it works in general, give the `man` program a try. It
takes as an argument the name of a program, and shows you its _manual
page_. Press `q` to exit.

```console
missing:~$ man ls
```

## Connecting programs

In the shell, programs have two primary "streams" associated with them:
their input stream and their output stream. When the program tries to
read input, it reads from the input stream, and when it prints
something, it prints to its output stream. Normally, a program's input
and output are both your terminal. That is, your keyboard as input and
your screen as output. However, we can also rewire those streams!

The simplest form of redirection is `< file` and `> file`. These let you
rewire the input and output streams of a program to a file respectively:

```console
missing:~$ echo hello > hello.txt
missing:~$ cat hello.txt
hello
missing:~$ cat < hello.txt
hello
missing:~$ cat < hello.txt > hello2.txt
missing:~$ cat hello2.txt
hello
```

Demonstrated in the example above, `cat` is a program that con`cat`enates
files. When given file names as arguments, it prints the contents of each of
the files in sequence to its output stream. But when `cat` is not given any
arguments, it prints contents from its input stream to its output stream (like
in the third example above).

You can also use `>>` to append to a file. Where this kind of
input/output redirection really shines is in the use of _pipes_. The `|`
operator lets you "chain" programs such that the output of one is the
input of another:

```console
missing:~$ ls -l / | tail -n1
drwxr-xr-x 1 root  root  4096 Jun 20  2019 var
missing:~$ curl --head --silent google.com | grep --ignore-case content-length | cut --delimiter=' ' -f2
219
```

We will go into a lot more detail about how to take advantage of pipes
in the lecture on data wrangling.

## A versatile and powerful tool

On most Unix-like systems, one user is special: the "root" user. You may
have seen it in the file listings above. The root user is above (almost)
all access restrictions, and can create, read, update, and delete any
file in the system. You will not usually log into your system as the
root user though, since it's too easy to accidentally break something.
Instead, you will be using the `sudo` command. As its name implies, it
lets you "do" something "as su" (short for "super user", or "root").
When you get permission denied errors, it is usually because you need to
do something as root. Though make sure you first double-check that you
really wanted to do it that way!

One thing you need to be root in order to do is writing to the `sysfs` file
system mounted under `/sys`. `sysfs` exposes a number of kernel parameters as
files, so that you can easily reconfigure the kernel on the fly without
specialized tools. **Note that sysfs does not exist on Windows or macOS.**

For example, the brightness of your laptop's screen is exposed through a file
called `brightness` under

```
/sys/class/backlight
```

By writing a value into that file, we can change the screen brightness.
Your first instinct might be to do something like:

```console
$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'
/sys/class/backlight/thinkpad_screen/brightness
$ cd /sys/class/backlight/thinkpad_screen
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
```

This error may come as a surprise. After all, we ran the command with
`sudo`! This is an important thing to know about the shell. Operations
like `|`, `>`, and `<` are done _by the shell_, not by the individual
program. `echo` and friends do not "know" about `|`. They just read from
their input and write to their output, whatever it may be. In the case
above, the _shell_ (which is authenticated just as your user) tries to
open the brightness file for writing, before setting that as `sudo
echo`'s output, but is prevented from doing so since the shell does not
run as root. Using this knowledge, we can work around this:

```console
$ echo 3 | sudo tee brightness
```

Since the `tee` program is the one to open the `/sys` file for writing,
and _it_ is running as `root`, the permissions all work out. You can
control all sorts of fun and useful things through `/sys`, such as the
state of various system LEDs (your path might be different):

```console
$ echo 1 | sudo tee /sys/class/leds/input6::scrolllock/brightness
```

# Next steps

At this point you know your way around a shell enough to accomplish
basic tasks. You should be able to navigate around to find files of
interest and use the basic functionality of most programs. In the next
lecture, we will talk about how to perform and automate more complex
tasks using the shell and the many handy command-line programs out
there.

# Exercises

All classes in this course are accompanied by a series of exercises. Some give
you a specific task to do, while others are open-ended, like "try using X and Y
programs". We highly encourage you to try them out.

We have not written solutions for the exercises. If you are stuck on anything
in particular, feel free to send us an email describing what you've tried so
far, and we will try to help you out.

 1. For this course, you need to be using a Unix shell like Bash or ZSH. If you
    are on Linux or macOS, you don't have to do anything special. If you are on
    Windows, you need to make sure you are not running cmd.exe or PowerShell;
    you can use [Windows Subsystem for
    Linux](https://docs.microsoft.com/en-us/windows/wsl/) or a Linux virtual
    machine to use Unix-style command-line tools. To make sure you're running
    an appropriate shell, you can try the command `echo $SHELL`. If it says
    something like `/bin/bash` or `/usr/bin/zsh`, that means you're running the
    right program.
 1. Create a new directory called `missing` under `/tmp`.
 1. Look up the `touch` program. The `man` program is your friend.
 1. Use `touch` to create a new file called `semester` in `missing`.
 1. Write the following into that file, one line at a time:
    ```
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```
    The first line might be tricky to get working. It's helpful to know that
    `#` starts a comment in Bash, and `!` has a special meaning even within
    double-quoted (`"`) strings. Bash treats single-quoted strings (`'`)
    differently: they will do the trick in this case. See the Bash
    [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
    manual page for more information.
 1. Try to execute the file, i.e. type the path to the script (`./semester`)
    into your shell and press enter. Understand why it doesn't work by
    consulting the output of `ls` (hint: look at the permission bits of the
    file).
 1. Run the command by explicitly starting the `sh` interpreter, and giving it
    the file `semester` as the first argument, i.e. `sh semester`. Why does
    this work, while `./semester` didn't?
 1. Look up the `chmod` program (e.g. use `man chmod`).
 1. Use `chmod` to make it possible to run the command `./semester` rather than
    having to type `sh semester`. How does your shell know that the file is
    supposed to be interpreted using `sh`? See this page on the
    [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more
    information.
 1. Use `|` and `>` to write the "last modified" date output by
    `semester` into a file called `last-modified.txt` in your home
    directory.
 1. Write a command that reads out your laptop battery's power level or your
    desktop machine's CPU temperature from `/sys`. Note: if you're a macOS
    user, your OS doesn't have sysfs, so you can skip this exercise.
