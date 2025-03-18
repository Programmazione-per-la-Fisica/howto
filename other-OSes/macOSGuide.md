# Configurazione dell'ambiente di lavoro su macOS

- [Configurazione dell'ambiente di lavoro su macOS](#configurazione-dellambiente-di-lavoro-su-macos)
  - [Prerequisito: Xcode e i Command Line Tools](#prerequisito-xcode-e-i-command-line-tools)
  - [Installazione di Homebrew](#installazione-di-homebrew)
  - [Installazione degli strumenti di base](#installazione-degli-strumenti-di-base)
  - [Installazione di Visual Studio Code](#installazione-di-visual-studio-code)
  - [Installazione di componenti aggiuntivi](#installazione-di-componenti-aggiuntivi)
  - [Aggiornamento dei software installati](#aggiornamento-dei-software-installati)
- [Risoluzione dei problemi](#risoluzione-dei-problemi)
  - [Non è possibile lanciare VSCode da terminale](#non-è-possibile-lanciare-vscode-da-terminale)
  - [Problemi di linking durante la compilazione con gcc](#problemi-di-linking-durante-la-compilazione-con-gcc)
  - [Metodi alternativi di compilazione del codice _C++_](#metodi-alternativi-di-compilazione-del-codice-c)
  - [Non è possibile utilizzare i comandi installati tramite Homebrew](#non-è-possibile-utilizzare-i-comandi-installati-tramite-homebrew)

Questa guida contiene le istruzioni da seguire per configurare, all'interno del sistema operativo _macOS_, un ambiente
di lavoro adatto al corso di Programmazione per la Fisica.

La configurazione risulta relativamente semplice, in quanto macOS è un sistema operativo per molti versi simile a Linux
e fa parte della famiglia Unix.

## Prerequisito: Xcode e i Command Line Tools

I _Command Line Tools (CLT) di Xcode_ sono necessari per procedere con l'installazione di tutti gli strumenti di lavoro.

In aggiunta è necessario effettuare un'installazione completa di _Xcode_ per installare il framework di analisi _ROOT_
il quale, sebbene non necessario durante questo corso, verrà utilizzato in altri insegnamenti.

Se non lo hai già fatto, puoi installare _Xcode_ seguendo queste istruzioni:

1. apri la pagina relativa ad [Xcode](https://apps.apple.com/us/app/xcode/id497799835) tramite il browser;
2. una volta aperta, segui le indicazioni e utilizza il programma _Mac App Store_ per procedere con l'installazione;
3. si avvierà una finestra di dialogo che ti permetterà di completare il processo.

A seconda delle risorse (ad es. connessione) disponibili, il processo può richiedere abbastanza tempo (alcune decine di
minuti o più).

Se possibile, **raccomandiamo di effettuare questa parte dell'installazione già a casa**, prima di presentarti in
laboratorio, dove saranno poi completati il resto dell'installazione e della configurazione.

## Installazione di Homebrew

Per l'installazione dei prodotti software necessari per il corso useremo principalmente il _package manager_
[`Homebrew`](https://brew.sh/) (in breve _brew_).

Per l'uso di brew sono richiesti alcuni prerequisiti:

- Un _Mac_ con processore 64-bit Intel o Apple Silicon
- macOS Ventura (13) o superiore
- i CLT di Xcode (o Xcode), la cui installazione è stata [appenda discussa](#prerequisito-xcode-e-i-command-line-tools)

Installa brew, aprendo l'applicazione Terminale (o Terminal) che si trova in Applicazioni &rarr; Utility (o Applications
&rarr; Utility) ed eseguendo il seguente comando:

```zsh
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> [!IMPORTANT]
> **Nota alla riga di comando**
>
> Quando indicato nel testo, potrebbe essere necessario inserire un comando da un'applicazione detta _Terminale_.
>
> In questa guida, tali comandi sono preceduti da un simbolo, chiamato `prompt`, che può variare in base al terminale
> utilizzato o al sistema operativo. Tipicamente su Windows il simbolo è `>`, su Linux `$` e su MacOs `%` (oppure `$`).
>
> È possibile individuare il prompt all'inizio della linea di comando quando il terminale è in attesa di istruzioni.
> Seppur riportato nella guida, non si deve inserire il simbolo di prompt nello scrivere i comandi presentati in
> seguito.
>
> Dopo aver inserito un comando è possibile eseguirlo battendo il tasto _Invio_.

> [!WARNING]
> Se, durante l'installazione, vedi errori relativi al comando `curl` che si lamenta di verifica di certificati,
> prova ad aprire l'URL corrispondente dentro Safari, visualizza il certificato e accettalo "fidandoti sempre". Poi
> riprova il comando indicato sopra.

> [!TIP]
> Per verificare che l'installazione di brew sia andata a buon fine, esegui il comando:
>
> ```zsh
> % brew
> ```
>
> In caso di successo, le prime righe dell'output riportato sul terminale dovrebbero essere simili a queste:
>
> ```zsh
> Example usage:
> brew search TEXT|/REGEX/
> brew info [FORMULA|CASK...]
> brew install FORMULA|CASK...
> brew update
> brew upgrade [FORMULA|CASK...]
> brew uninstall FORMULA|CASK...
> brew list [FORMULA|CASK...]
> ...
> ```
>
> Qualora, invece, il Terminale si lamenti dell'assenza del comando `brew`:
>
> ```zsh
> % brew
> zsh: command  not found: brew
> ```
>
> per terminare l'installazione potrebbe essere necessario eseguire alcuni comandi aggiuntivi.
>
> Le istruzioni esatte **sono riportate, sul Terminale, nelle ultime righe dell'output del comando installazione**.

## Installazione degli strumenti di base

Una volta terminata l'installazione di brew, puoi installare gli strumenti software necessari per il corso.

Innanzitutto, verifica la versione più recente disponibile del compilatore _gcc_ (verosimilmente, la versione 14):

```zsh
% brew info gcc
==> gcc: stable 14.2.0 (bottled), HEAD
GNU compiler collection
https://gcc.gnu.org/
...
```

e **prendi nota** del primo numero, tra i tre separati da punti nella prima riga di output (in questo caso 14:
`==> gcc: stable 14.2.0 (bottled), HEAD`)
  
Poi, installa i seguenti pacchetti:

```zsh
% brew install git gcc clang-format
```

Questo comando, nell'ordine, installa:

- il _version control system_ [git](https://git-scm.com/)
- il compilatore [gcc](https://gcc.gnu.org/)
- [clang-format](https://www.kernel.org/doc/html/latest/translations/it_IT/process/clang-format.html), uno strumento che
  verifica la buona formattazione del codice

> [!WARNING]
> Il comando che gli utenti macOS utilizzeranno per la compilazione del codice C++ **contiene il numero che ti abbiamo
> chiesto di annotare poco fa**: nel caso della presente guida il comando è `g++-14` (tutto attaccato), non  `g++`,
> come verrà di solito indicato durante il corso.
>
> Il comando `g++` è probabilmente disponibile, ma è un _alias_ per un altro compilatore (se vuoi puoi leggere
> [questa parte della guida](#metodi-alternativi-di-compilazione-del-codice-c) per una descrizione dettagliata).

> [!TIP]
>
> Per verificare la corretta installazione dei pacchetti appena descritti, eseguire i seguenti comandi:
>
> ```zsh
> % git --version
> git version 2.46.1
> ```
>
> ```zsh
> % g++-14 --version
> g++-14 (Homebrew GCC 14.2.0) 14.2.0
> Copyright (C) 2024 Free Software Foundation, Inc.
> This is free software; see the source for copying conditions.  There is NO
> warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
> ```
>
> ```zsh
> % clang-format --version
> clang-format version 19.1.0
> ```
>
> I numeri di versione riportati sopra sono solo indicativi, e possono variare nel tempo, **quello che è importante**
> è che **nessuno dei tentativi** di esecuzione **termini con un errore del tipo** `zsh: command not found`.

## Installazione di Visual Studio Code

Per l'installazione di _Visual Studio Code_ (VSCode) scarica il pacchetto dalla
[pagina](https://code.visualstudio.com/) corrispondente.

Alcune note in merito all'installazione:

- ricorda di copiare l'applicazione `Visual Studio Code.app` dentro la cartella Applicazioni (Applications) come
  descritto [qui](https://code.visualstudio.com/docs/setup/mac#_installation)
- abilita l'esecuzione dell'applicazione da Terminale seguendo le istruzioni riportate
    [qui](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)

> [!TIP]
>
> Per verificare la corretta installazione di VSCode, provare ad aprirlo eseguendo il seguente comando
>
> ```zsh
> % code .
> ```
>
> Se l'installazione è stata eseguita correttamente, si avvierà la finestra di VSCode.

## Installazione di componenti aggiuntivi

Più avanti nel corso, faremo uso di strumenti aggiuntivi, quali:

- [CMake](https://cmake.org/): un software libero multipiattaforma che automatizza la compilazione di progetti complessi
- [SFML](https://www.sfml-dev.org/): una libreria multimediale (che utilizzeremo per lo sviluppo di applicazioni
  grafiche)

Nel caso di macOS, è possibile installare anche queste componenti aggiuntive tramite `brew`:

```zsh
% brew install cmake sfml
```

> [!TIP]
> Per verificare la corretta installazione dei componenti aggiuntivi, eseguite i seguenti comandi:
>
> ```zsh
> % cmake --version
> cmake version 3.30.3
>
> CMake suite maintained and supported by Kitware (kitware.com/cmake).
> ```
>
> ```zsh
> % brew list sfml
> /opt/homebrew/Cellar/sfml/2.6.1/include/SFML/ (109 files)
> /opt/homebrew/Cellar/sfml/2.6.1/lib/libsfml-audio.2.6.1.dylib
> /opt/homebrew/Cellar/sfml/2.6.1/lib/libsfml-graphics.2.6.1.dylib
> /opt/homebrew/Cellar/sfml/2.6.1/lib/libsfml-network.2.6.1.dylib
> ...
> ```
>
> e verificare che l'output, a meno di numeri di versione, sia consistente con quello riportato in questa guida.

## Aggiornamento dei software installati

È buona norma **aggiornare periodicamente**, indicativamente **una volta alla settimana**, tutti i pacchetti
software installati.

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

> [!WARNING]
> La situazione è ben diversa quando si parla di update della release del sistema operativo (ad es. il passaggio da
> _macOS Big Sur_ a _macOS Monterey_).
> **Prima di procedere ad un cambiamento tanto radicale** è buona norma
> **assicurarsi in anticipo che i programmi che utilizziamo**
> normalmente **siano compatibili con la nuova versione del sistema operativo**.
>
> Nel caso di programmi installati tramite `brew`, possiamo effettuare tale verifica utilizzando questa
> [pagina web](https://formulae.brew.sh/formula/)
> (prova, ad esempio, a verificare le compatibilità per il compilatore [`gcc`'](https://formulae.brew.sh/formula/gcc)).

# Risoluzione dei problemi

## Non è possibile lanciare VSCode da terminale

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

> [!NOTE]
> Qualora ti venga richiesto di digitare la password, o di confermare il comando utilizzando il lettore di impronte
> digitali, procedi pure senza esitazioni.

A questo punto, prova di nuovo ad eseguire il comando `code` da terminale:

```zsh
% code
```

## Problemi di linking durante la compilazione con gcc

Qualora, durante la compilazione con `g++-14`, riscontrassi errori di _linking_ simili a:

```zsh
% g++-14 -Wall -Wextra hello.cpp -o hello 
ld: warning: ignoring duplicate libraries: '-lgcc'
0  0x102597648  __assert_rtn + 72
1  0x1024cbfac  ld::AtomPlacement::findAtom(unsigned char, unsigned long long, ld::AtomPlacement::AtomLoc const*&, long long&) const + 1204
2  0x1024e1924  ld::InputFiles::SliceParser::parseObjectFile(mach_o::Header const*) const + 15164
3  0x1024eee30  ld::InputFiles::parseAllFiles(void (ld::AtomFile const*) block_pointer)::$_7::operator()(unsigned long, ld::FileInfo const&) const + 420
4  0x1ab410440  _dispatch_client_callout2 + 20
5  0x1ab423f1c  _dispatch_apply_invoke + 224
6  0x1ab410400  _dispatch_client_callout + 20
7  0x1ab421fb8  _dispatch_root_queue_drain + 684
8  0x1ab4226c0  _dispatch_worker_thread2 + 164
9  0x1ab5bc038  _pthread_wqthread + 228
ld: Assertion failed: (resultIndex < sectData.atoms.size()), function findAtom, file Relocations.cpp, line 1336.
collect2: error: ld returned 1 exit status
```

> [!NOTE]
> Gli errori potrebbero essere diversi ma, si dovrebbero riferire alla fase di linking, ovvero iniziare con `ld: ...`.

Puoi tentare di compilare il codice aggiungendo al comando `g++-14` la seguente opzione `-Wl,-ld_classic`, lasciando
tutte le altre opzioni e gli argomenti che avresti utilizzato per la compilazione invariati, ad esempio:

```zsh
% g++-14 -Wl,-ld_classic -Wall -Wextra hello.cpp -o hello 
```

Qualora questo suggerimento non dovesse risolvere il problema, prova la soluzione proposta [qui](#metodi-alternativi-di-compilazione-del-codice-c).

## Metodi alternativi di compilazione del codice _C++_

Come discusso in questa guida e ripetuto durante i laboratori, chi usa mac OS dovrebbe preferenzialmente utilizzare il
comando `g++-14` per la compilazione del codice sviluppato.

In caso questo non funzioni, nel breve periodo (es.: durante un dato laboratorio), puoi tentare di compilare il codice
sostituendo al comando `g++-14` la seguente coppia di comando e opzione `g++ -std=c++17`, lasciando tutte le altre
opzioni e gli argomenti che avresti utilizzato per la compilazione invariati.

In ogni caso, nel medio termine (es.: nei giorni successivi al laboratorio), il problema con `g++-14` va risolto.
Riferisciti alle istruzioni [qui sotto](#non-è-possibile-utilizzare-i-comandi-installati-tramite-homebrew) e sentiti
libero di contattare [i docenti](https://virtuale.unibo.it/mod/page/view.php?id=1045205)

## Non è possibile utilizzare i comandi installati tramite Homebrew

Qualora, i programmi installati tramite `brew` smettano di funzionare (ad es.: `gcc`, `root`, etc ...), per prima cosa
puoi verificare è lo stato generale del package manager tramite il comando:

```zsh
% brew doctor
Your system is ready to brew.
```

Qualora l'output del comando sia differente da quello di cui sopra, `brew doctor` dovrebbe comunque fornirti
suggerimenti in merito a come procedere.

In caso `brew doctor` non aiuti, puoi tentare le seguenti azioni:

> [!TIP]
> Per qualsiasi dubbio, o anche solo perché preferisci che qualcuno ti assista durante i tentativi, puoi sempre
> contattare [i titolari dei moduli di laboratorio](https://virtuale.unibo.it/mod/page/view.php?id=1045205) del corso.

**Aggiornare la versione di `brew` e i pacchetti installati:**

Come discusso sopra, puoi farlo eseguendo i comandi:

```zsh
% brew update
% brew upgrade
```

**Verificare lo stato di installazione degli xcode CLT:**

In primis esegui il comando:

```zsh
% xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

In caso sia necessaria una nuova installazione, il comando eseguito provvederà ad iniziarla.

In caso il comando restituisca l'output che abbiamo riportato, puoi verificare la presenza di aggiornamenti da
installare con:

```zsh
% softwareupdate --list       
Software Update Tool

Finding available software
No new software available.
```

In caso caso ci siano aggiornamenti da effettuare (nel caso mostrato sopra non ce ne sono), e tra questi risultino i CLT
o Xcode, puoi installarli tramite il seguente comando::

```zsh
% softwareupdate --install -v <nome nel programma da installare>
```

> [!WARNING]
> Come riportato sopra, qualora vengano proposti da `softwareupdate` evita aggiornamenti della release del
> sistema operativo (ad es. il passaggio da _macOS Big Sur_ a _macOS Monterey_).

**Reinstallare `brew`  i pacchetti installati tramite il package manager**

In rari casi, i processi di aggiornamento del sistema operativo o di Xcode,
possono portare i pacchetti installati tramite _Homebrew_ in uno stato
inconsistente, che il comando `brew doctor` non riesce a riconoscere.

Questo potrebbe portarti in condizioni tali da non riuscire a compilare o usare
correttamente librerie come _SFML_ o programmi come _ROOT_.

Pertanto, potresti voler tentare una reinstallazione di _Homebrew_ e tutti
i pacchetti tramite esso installati.

La lista dei comandi è documentata in seguito, ma, in particolar modo in questo
caso, ti **consigliamo vivamente** di **contattare
[i docenti](https://virtuale.unibo.it/mod/page/view.php?id=1045205)** prima di
procedere:

```zsh
% brew bundle dump
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
% brew bundle install
```
