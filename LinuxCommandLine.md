# Basics of the linux command line

A basic tutorial can be found here:

* <https://ubuntu.com/tutorials/command-line-for-beginners>
* We'll only really need up to section 5
* This tutorial is based on ubuntu - but everything is the same for any flavour of linux, including the CentOS that runs on smp-teaching.
* Essentially everything is also the same on MacOS

A handy list of common command-line commands:

The manual pages on the computer can be accessed by typing man and the command name, eg.
“man pwd”. This tells you what each command does, good to do before you try each of the following
commands:

| Syntax    | Description |
| --------- | ----------- |
| pwd       | prints current directoty [Print Working Directory]  |
| ls        | lists all files/directories in current directory |
| mkdir     | creates a new directory |
| cp        | copy a file |
| mv        | move (rename) a file |
| touch     | creates a new (blank) file |
| rm        | deletes a file (be **very** careful, there is NO recylce bin) |
| less      | prints the contents of a file to the terminal |
| cd        | change directory |
| .         | a '.' is short-hand for current directory |
| ..        | short-hand for parent (one-up) directory |
| ~         | shortcut for your home directory |
| g++       | runs the g++ compiler |
| gnuplot   | opens plotting program |
|           |  from inside gnuplot, try (e.g.) `gnuplot>plot sin(x)` |
|           | type 'quit' or 'exit' to close gnuplot |
| <kbd>tab</kbd> | he tab key is very useful - it is autocomplete. It will save you from typing long file names, and will help avoid making typos!|

In a Terminal try typing in the following commands in order, and see if you can follow what is hapenning and why. If you don't understand what they are doing, please ask one of us for help:

```bash
 pwd
 ls
 mkdir temp
 ls
 cd temp
 pwd
 ls
 touch hello.txt
 ls
 cp hello.txt hello2.txt
 ls
 cd ..
 pwd
 cd ~
 pwd
```
