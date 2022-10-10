# Configurazione dell'ambiente di lavoro su macOS

- [Configurazione dell'ambiente di lavoro su macOS](#configurazione-dellambiente-di-lavoro-su-macos)
  - [Prerequisito: i Command Line Tools di Xcode](#prerequisito-i-command-line-tools-di-xcode)
  - [Installazione di Homebrew](#installazione-di-homebrew)
  - [Installazione degli strumenti di base](#installazione-degli-strumenti-di-base)
  - [Installazione di Visual Studio Code](#installazione-di-visual-studio-code)
  - [Installazione di componenti aggiuntivi](#installazione-di-componenti-aggiuntivi)
  - [Aggiornamenti dei software installati](#aggiornamenti-dei-software-installati)
  - [Risoluzione dei problemi](#risoluzione-dei-problemi)
    - [Non è possibile lanciare VSCode da terminale](#non-è-possibile-lanciare-vscode-da-terminale)
    - [Non è possibile utilizzare i comandi installati tramite Homebrew](#non-è-possibile-utilizzare-i-comandi-installati-tramite-homebrew)

Questa guida contiene le istruzioni da seguire per configurare, all'interno del sistema operativo _macOS_, un ambiente di
lavoro adatto al corso di Programmazione per la Fisica.

La configurazione risulta relativamente semplice, in quanto macOS è un sistema operativo per molti versi simile a Linux
e fa parte della famiglia Unix.

> **Nota alla riga di comando**
>
> Quando indicato nel testo, potrebbe essere necessario inserire un comando da un'applicazione detta _Terminale_.
>
> In questa guida, tali comandi sono preceduti da un simbolo, chiamato `prompt`, che può variare in base al terminale
> utilizzato o al sistema operativo. Tipicamente su Windows il simbolo è `>`, su Linux `$` e su MacOs `%` (oppure `$`).
>
> È possibile individuare il prompt all'inizio della linea di comando quando il terminale è in attesa di istruzioni.
> Seppur riportato nella guida, non si deve inserire il simbolo di prompt nello scrivere i comandi presentati in seguito.
>
> Dopo aver inserito un comando è possibile eseguirlo battendo il tasto _Invio_.

## Prerequisito: i Command Line Tools di Xcode

I _Command Line Tools (CLT) di Xcode_ sono necessari per procedere con l'installazione di tutti gli strumenti di lavoro.

Se non hai già installato i CLT, puoi farlo seguendo queste istruzioni:

1. apri l'applicazione Terminale (o Terminal) che si trova in Applicazioni &rarr; Utility (o Applications &rarr; Utility)
2. una volta aperta, esegui il comando: `xcode-select --install` (ricordati di premere invio dopo aver copiato la riga)
3. si avvierà una finestra di dialogo che ti permette di effettuare l'installazione.

Alternativamente, puoi ottenere i CLT in uno dei seguenti modi (le opzioni sono esclusive):

- scarica il prodotto da [https://developer.apple.com/downloads](https://developer.apple.com/downloads)
- come parte di [Xcode](https://itunes.apple.com/us/app/xcode/id497799835) stesso

A seconda dell'opzione scelta e delle risorse (ad es. connessione) disponibili, il processo può richiedere abbastanza
tempo (alcune decine di minuti o più). Questo vale sia per un'installazione completa di Xcode, sia in caso ci si limiti
all'installazione dei CLT.

Pertanto **raccomandiamo di effettuare questa parte dell'installazione già a casa**, prima di presentarsi in laboratorio,
dove saranno poi completati il resto dell'installazione e della configurazione.

## Installazione di Homebrew

Per l'installazione dei prodotti software necessari per il corso useremo principalmente il _package manager_ [`Homebrew`](https://brew.sh/)
(in breve _brew_).

Per l'uso di brew sono richiesti alcuni prerequisiti:

- macOS Catalina (10.15) o superiore
- i CLT di Xcode, la cui installazione è stata [appenda discussa](#prerequisito-i-command-line-tools-di-xcode)

Una volta installati i CLT, installa brew eseguendo, sempre sul Terminale, il seguente comando:

```zsh
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Se, durante l'installazione, vedi errori relativi al comando `curl` che si lamenta di verifica di certificati,
prova ad aprire l'URL corrispondente dentro Safari, visualizza il certificato e accettalo "fidandoti sempre". Poi
riprova il comando indicato sopra.

Per verificare che l'installazione di brew sia andata a buon fine, esegui il comando:

```zsh
% brew
```

In caso di successo, le prime righe dell'output riportato sul terminale dovrebbero essere simili a queste:

```zsh
Example usage:
  brew search TEXT|/REGEX/
  brew info [FORMULA|CASK...]
  brew install FORMULA|CASK...
  brew update
  brew upgrade [FORMULA|CASK...]
  brew uninstall FORMULA|CASK...
  brew list [FORMULA|CASK...]
  ...
```

Qualora, invece, il Terminale si lamenti dell'assenza del comando `brew`:

```zsh
% brew
zsh: command  not found: brew
```

per terminare l'installazione potrebbe essere necessario eseguire alcuni comandi aggiuntivi.

Le istruzioni esatte **sono riportate, sul Terminale, nelle ultime righe dell'output del comando installazione**.

## Installazione degli strumenti di base

Una volta terminata l'installazione di brew, puoi installare gli strumenti software necessari per il corso.

Innanzitutto, verifica la versione più recente disponibile del compilatore _gcc_ (verosimilmente, la versione 12):

```zsh
% brew info gcc
==> gcc: stable 12.2.0 (bottled), HEAD
GNU compiler collection
https://gcc.gnu.org/
...
```

Poi, installa i seguenti pacchetti:

```zsh
% brew install git gcc clang-format
```

Questo comando, nell'ordine, installa:

- il _version control system_ [git](https://git-scm.com/)
- il compilatore [gcc](https://gcc.gnu.org/)
- [clang-format](https://www.kernel.org/doc/html/latest/translations/it_IT/process/clang-format.html), uno strumento che
  verifica la buona formattazione del codice

Il comando che gli utenti macOS utilizzeranno per la compilazione del codice C++ è `g++-12` (tutto attaccato), non `g++`,
come verrà di solito indicato durante il corso. Per questo motivo, poco sopra, abbiamo verificato la versione di `gcc`.

> :warning: Il comando `g++` è probabilmente disponibile, ma è un _alias_ per un altro compilatore.
> Qualora ti venisse suggerito durante il corso di utilizzare quest'ultimo al posto di  gcc, sarà necessario specificare esplicitamente
> l'opzione di compilazione `-std=c++17`; il comando da utilizzare diventerebbe quindi  `g++ -std=c++17`.

Per verificare la corretta installazione dei pacchetti appena descritti, eseguire i seguenti comandi:

```zsh
% git --version
git version 2.37.3
```

```zsh
g++-12 --version
g++-12 (Homebrew GCC 12.2.0) 12.2.0
Copyright (C) 2022 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

```zsh
% clang-format --version
clang-format version 14.0.6
```

I numeri di versione riportati sopra sono solo indicativi, e possono variare nel tempo, quello che è importante è che nessuno
dei tentativi di esecuzione termini con un errore del tipo `zsh: command not found`.

## Installazione di Visual Studio Code

Per l'installazione di _Visual Studio Code_ (VSCode) scarica il pacchetto dalla
[pagina](https://code.visualstudio.com/) corrispondente.

Alcune note in merito all'installazione:

- ricorda di copiare l'applicazione `Visual Studio Code.app` dentro la cartella Applicazioni (Applications) come
  descritto [qui](https://code.visualstudio.com/docs/setup/mac#_installation)
- abilita l'esecuzione dell'applicazione da Terminale seguendo le istruzioni riportate
    [qui](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)

Per verificare la corretta installazione di VSCode, provare ad aprirlo eseguendo il seguente comando

```zsh
% code
```

Se l'installazione è stata eseguita correttamente, si avvierà la finestra di VSCode.

## Installazione di componenti aggiuntivi

Più avanti nel corso, faremo uso di strumenti aggiuntivi, quali:

- [CMake](https://cmake.org/): un software libero multipiattaforma che automatizza la compilazione di progetti complessi
- [SFML](https://www.sfml-dev.org/): una libreria multimediale (che utilizzeremo per lo sviluppo di applicazioni
  grafiche)

Nel caso di macOS, è possibile installare anche queste componenti aggiuntive tramite `brew`:

```zsh
% brew install cmake sfml
```

## Aggiornamenti dei software installati

È buona norma aggiornare periodicamente, indicativamente una volta alla settimana, tutti i pacchetti software
installati.

Nel caso delle componenti installate tramite brew, l'aggiornamento si effettua
[eseguendo i seguenti comandi](https://docs.brew.sh/FAQ#how-do-i-update-my-local-packages):

```zsh
% brew update
% brew upgrade
```

Il primo comando aggiorna il programma `brew` e la lista dei pacchetti (detti _formulae_) disponibili. Il secondo
effettua l'aggiornamento dei pacchetti installati.

Prima di eseguire il comando `brew upgrade`, puoi controllare la lista dei pacchetti che verranno aggiornati col
comando:

```zsh
% brew outdated
```

> :warning: La situazione è ben diversa quando si parla di update della release del sistema operativo (ad es.
> il passaggio da _macOS Big Sur_ a _macOS Monterey_).
> **Prima di procedere ad un cambiamento tanto radicale** è buona norma **assicurarsi in anticipo che i programmi che utilizziamo**
> normalmente **siano compatibili con la nuova versione del sistema operativo**.
>
> Nel caso di programmi installati tramite `brew`, possiamo effettuare tale verifica utilizzando questa [pagina web](https://formulae.brew.sh/formula/)
> (prova, ad esempio, a verificare le compatibilità per il compilatore [`gcc`'](https://formulae.brew.sh/formula/gcc)).

## Risoluzione dei problemi

### Non è possibile lanciare VSCode da terminale

Qualora, lanciando il comando `code` da terminale, tu incorra in un errore simile a:

```zsh
% code
zsh: command not found: code
```

procedi come segue:

1. apri la _Command Palette_ di VSCode utilizzando la _combinazione di tasti_
   <kbd>Cmd</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> ed esegui il comando che trovi digitando `uninstall code from path`
2. prova di nuovo ad abilitare l'esecuzione dell'applicazione da Terminale  seguendo le istruzioni riportate
   [qui](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)

> :warning: Qualora ti venga richiesto di digitare la password, o di confermare il comando utilizzando il lettore di
> impronte digitali, procedi pure senza esitazioni.

A questo punto, prova di nuovo ad eseguire il comando `code` da terminale:

```zsh
% code
```

### Non è possibile utilizzare i comandi installati tramite Homebrew

Qualora, i programmi installati tramite `brew` smettano di funzionare (ad es.: `gcc`, `root`, etc ...), per
prima cosa puoi verificare è lo stato generale del package manager tramite il comando:

```zsh
% brew doctor
Your system is ready to brew.
```

Qualora l'output del comando sia differente da quello di cui sopra, `brew doctor` dovrebbe comunque fornirti
suggerimenti in merito a come procedere. In caso questi non siano chiari, o per qualsiasi dubbio, contatta
[i titolari dei moduli di laboratorio](mailto:carlo.battilana2@unibo.it,fabio.ferrari17@unibo.it) del corso.
