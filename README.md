<!-- omit in toc -->
# Howto

- [Piattaforma di riferimento](#piattaforma-di-riferimento)
- [Strumenti software necessari](#strumenti-software-necessari)
- [Altre piattaforme](#altre-piattaforme)
- [Editor](#editor)
- [Introduzione a Linux e all'uso della shell](#introduzione-a-linux-e-alluso-della-shell)
- [Appendice: ROOT](#appendice-root)

Questa repository contiene la documentazione necessaria per configurare
l'ambiente di lavoro per l'insegnamento di
_[Programmazione per la Fisica](https://github.com/Programmazione-per-la-Fisica/pf2023)_,
corso di laurea in Fisica, Università di Bologna, Anno Accademico 2023/2024.

Il contenuto della repository è scaricabile sul proprio computer usando il
comando `git`:

```shell
git clone https://github.com/Programmazione-per-la-Fisica/howto.git
```

## Piattaforma di riferimento

La piattaforma di riferimento del corso è la distribuzione
**Linux Ubuntu 22.04**.

## Strumenti software necessari

Gli strumenti software minimi richiesti sono:

- shell: `bash`
- version control: `git`
- compilatore C++: `g++`
- formattatore di codice: `clang-format`
- editor/IDE: _Visual Studio Code_ ([vivamente consigliato](#editor), possibili
  alternative sono: `nano`, `vi`, `emacs`)

La shell è disponibile già con l'installazione di default di Ubuntu. Gli altri
strumenti sono disponibili nel catalogo ufficiale dei pacchetti software della
distribuzione. Per l'installazione si usa il comando `apt`; ad esempio per
installare `git`, `g++` e `clang-format` è sufficiente eseguire il seguente
comando:

```shell
sudo apt install git g++ clang-format
```

Viene richiesta la password utente.

Durante il corso verranno usati ulteriori strumenti:
[`CMake`](https://cmake.org/) come _build system_ e
[SFML](https://sfml-dev.org/) per la creazione di semplici interfacce grafiche.
L'installazione è altrettanto semplice:

```shell
sudo apt install cmake libsfml-dev
```

## Altre piattaforme

Prodotti software analoghi sono disponibili su altre piattaforme di uso comune,
quali Windows e macOS:

- **Windows**: si suggerisce di installare il _Windows Subsystem for Linux_,
  seguendo [questa guida](other-OSes/WSLGuide.md);
- **macOS**: essendo simile a Linux, la configurazione è semplificata ed è
  illustrata in [questa guida](other-OSes/macOSGuide.md).

## Editor

Per uniformità tra tutte le piattaforme, l'editor consigliato è _[Visual Studio
Code](https://code.visualstudio.com/)_. Si rimanda alla pagina indicata per
l'installazione.

## Introduzione a Linux e all'uso della shell

Per prendere familiarità con Linux si suggeriscono le seguenti guide:

- [Introduzione a
  Linux](https://www.sci.unich.it/~amato/teaching/old/labdati10/lezioni/linux/linux.php)
  è una sintetica introduzione a Linux e alla shell, scritta dal prof. Gianluca
  Amato dell'Università di Chieti per un corso di "Laboratorio di Sistemi
  Operativi". Il testo è un po' datato e la pagina presenta qualche errore di
  formattazione, ma il contenuto è ancora valido.
- [Linux tutorial](https://ryanstutorials.net/linuxtutorial/) è una guida
  esauriente a Linux e alla Bash scritta da Ryan Chadwick. I capitoli "The
  Command Line", "Basic Navigation", "File Manipulation" contengono informazioni
  essenziali; gli altri possono essere approfonditi con calma; alcuni ("Vi Text
  Editor", "Scripting") possono essere considerati superflui per questo corso
  (ma comunque utili).

## Appendice: ROOT

Oltre agli strumenti necessari per il corso, sono fornite
[delle guide](ROOT-installation) per l'installazione del [framework di analisi
_ROOT_](https://root.cern/), che verrà utilizzato in altri insegnamenti del
corso di laurea in Fisica.
