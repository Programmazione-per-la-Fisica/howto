# Configurazione dell'ambiente di lavoro su Windows

- [Configurazione dell'ambiente di lavoro su Windows](#configurazione-dellambiente-di-lavoro-su-windows)
  - [Prerequisiti: verifica della Build di Windows e download di Ubuntu dal Microsoft Store](#prerequisiti-verifica-della-build-di-windows-e-download-di-ubuntu-dal-microsoft-store)
  - [Installazione di WSL 2 - Build 19041 o superiore](#installazione-di-wsl-2---build-19041-o-superiore)
  - [Installazione manuale WSL 2 - Build 18362 o superiori](#installazione-manuale-wsl-2---build-18362-o-superiori)
  - [Installazione manuale WSL 1 - Build da 16215 a 18360](#installazione-manuale-wsl-1---build-da-16215-a-18360)
  - [Configurare la distribuzione](#configurare-la-distribuzione)
    - [Installazione degli strumenti di base](#installazione-degli-strumenti-di-base)
  - [Installazione di Visual Studio Code](#installazione-di-visual-studio-code)
    - [Aprire una cartella remota](#aprire-una-cartella-remota)
  - [Verificare il funzionamento dell'interfaccia grafica](#verificare-il-funzionamento-dellinterfaccia-grafica)
  - [Risoluzione dei problemi](#risoluzione-dei-problemi)
    - [Fallimento nella creazione dello user su Ubuntu](#fallimento-nella-creazione-dello-user-su-ubuntu)
    - [Reset della password in Ubuntu](#reset-della-password-in-ubuntu)
    - [sudo apt update fallisce "Temporary failure resolving 'archive.ubuntu.com'"](#sudo-apt-update-fallisce-temporary-failure-resolving-archiveubuntucom)
    - [Impossibile avviare la macchina virtuale perché una funzionalità richiesta non è installata](#impossibile-avviare-la-macchina-virtuale-perché-una-funzionalità-richiesta-non-è-installata)
    - [Impossibile avviare VSCode su WSL con il comando `code`](#impossibile-avviare-vscode-su-wsl-con-il-comando-code)
    - [Passare file tra Windows e WSL](#passare-file-tra-windows-e-wsl)
      - [Accedere a Windows file system da WSL](#accedere-a-windows-file-system-da-wsl)
      - [Accedere al filesystem Linux da Windows](#accedere-al-filesystem-linux-da-windows)
    - [Cambiare la versione di WSL](#cambiare-la-versione-di-wsl)
    - [Aggiornare la distribuzione di Ubuntu](#aggiornare-la-distribuzione-di-ubuntu)

Questa guida descrive i passi necessari per configurare la propria macchina _Windows_ in preparazione per il corso di
Programmazione per la Fisica.

La procedura comporterà l'installazione dei seguenti strumenti software:

- [Windows Subsystem for Linux](https://docs.microsoft.com/it-it/windows/wsl/) (WSL) - che permette di eseguire un
  ambiente GNU/Linux direttamente in Windows;
- [Visual Studio Code](https://code.visualstudio.com/) - un editor di codice sorgente, disponibile sia per Windows che
  per macOS e Linux;

Con questi due strumenti è possibile lavorare in un ambiente Linux, utilizzando strumenti da riga di comando,
direttamente in Windows, senza ricorrere a soluzioni più complesse, quali macchine virtuali o configurazioni dual boot
(che sono comunque opzioni accettate).

Oltre ai programmi appena menzionati, troverete informazioni in merito all'installazione degli strumenti necessari
durante il corso.

> [!NOTE]
> **Nota alla riga di comando**
>
> Quando indicato nel testo, potrebbe essere necessario inserire un comando da un'applicazione detta _Terminale_. In
> questa guida i comandi sono preceduti da un simbolo detto `prompt`, che può variare in base al terminale utilizzato o
> al sistema operativo. Tipicamente su Windows il simbolo è `>`, su Linux `$` e su MacOs `%`.
>
> È possibile individuare il prompt all'inizio della linea di comando quando il terminale è in attesa di istruzioni.
> Seppur riportato, non si deve inserire il simbolo di prompt nello scrivere i comandi presentati in questa guida.
>
> Dopo aver inserito un comando è possibile eseguirlo battendo il tasto _Invio_.

> [!WARNING]
> In caso di problemi con l'installazione, fai riferimento a [questa
> guida](https://docs.microsoft.com/it-it/windows/wsl/install-win10#troubleshooting-installation).

## Prerequisiti: verifica della Build di Windows e download di Ubuntu dal Microsoft Store

Le istruzioni per l'installazione di WSL (nonché la versione di WSL disponibile) variano in base alla versione di
Windows installata sulla macchina.
Prima di proseguire, controlla quindi la versione di Windows navigando in Impostazioni -> Sistema -> Informazioni sul
sistema, ed annota il numero relativo a **Build sistema operativo**.

Se possibile, **ti raccomandiamo di effettuare questa parte dell'installazione già a casa**, prima di presentarti in
laboratorio, dove saranno poi completati il resto dell'installazione e della configurazione.

## Installazione di WSL 2 - Build 19041 o superiore

Se il proprio sistema operativo è aggiornato a Windows 11 (a partire dalla versione Preview 19041, fino alle versioni
_stable_ più recenti), è possibile utilizzare il comando semplificato di installazione.

> [!CAUTION]
> Prima dell'installazione, assicurarsi che gli strumenti di Virtualizzazione di Windows
> siano attivi. Per farlo è sufficiente cercare nella barra Start `features`, aprendo
> l'opzione `Attiva o disattiva funzionalità di Windows`. Da li assicurarsi che
> `Piattaforma macchina virtuale` e `Piattaforma Windows Hypervisor` siano attive.
> Se non lo fossero, attivarle e cliccare OK. Il computer si riavvierà al termine.

Per farlo è necessario aprire Powershell come Amministratore e lanciare il comando.

```cmd
> wsl.exe --install -d Ubuntu-24.04
```

Dopo un riavvio, WSL sarà pronta all'uso.

> [!NOTE]
>
> È possibile che venga nuovamente aperta una finestra del terminale dopo il riavvio.
> Lasciar terminare l'installazione fino al passaggio della creazione dell'account personale in Ubuntu.

Una volta installato il Sottosistema Windows per Linux passare alla sezione
[Configurare la distribuzione](#configurare-la-distribuzione) di questa guida.

## Installazione manuale WSL 2 - Build 18362 o superiori

**Abilita Windows Subsystem for Linux** aprendo: Pannello di controllo -> Programmi e funzionalità -> Attivazione o
disattivazione delle funzionalità Windows e selezionando _Sottosistema Windows per Linux_ (_Windows Subsystem for
Linux_).

> [!NOTE]
>
> Se, **in alternativa**, preferisci usare la linea di comando, apri Powershell come Amministratore e copia il seguente
> comando:
>
> ```powershell
> > dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
> ```
>
> Eseguilo premendo Invio, per abilitare la funzionalità facoltativa Sottosistema Windows per Linux.

**Abilita la Virtual Machine**, sempre dal menù Attivazione o disattivazione delle funzionalità Windows, selezionando
_Piattaforma macchina virtuale_ (_Virtual machine platform_).

> [!NOTE]
>
> Se, **in alternativa**, preferisci usare la linea di comando, apri Powershell come Amministratore e copia il seguente
> comando:
>
> ```powershell
> > dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
> ```
>
> Eseguilo premendo Invio, per abilitare la funzionalità facoltativa Piattaforma macchina virtuale.

**Premi OK** per applicare le modifiche e, al termine dell'installazione, **riavvia il dispositivo**.

**Scarica il Kernel Linux**  al link
[WSL2 Linux kernel update package for x64 machines](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
e **installalo**.

**Imposta WSL2 come versione predefinita** aprendo Powershell come amministratore ed eseguendo il seguente comando:

```powershell
> wsl --set-default-version 2
```

> [!NOTE]
> Premi Invio per eseguire il comando.

Una volta installato il Sottosistema Windows per Linux passare alla sezione
[Configurare la distribuzione](#configurare-la-distribuzione) di questa guida.

## Installazione manuale WSL 1 - Build da 16215 a 18360

Per il corso di programmazione per la fisica è suggerito utilizzare WSL2. Nel caso in cui il proprio dispositivo non lo
supporti e non sia possibile aggiornare la versione di Windows installata, è possibile installare la versione precedente
di WSL.

Per installare WSL1 seguire i soli passaggi 1, 3 e 6 presentati nella sezione [precedente](#installazione-manuale-wsl-2---build-18362-o-superiori).

## Configurare la distribuzione

Avvia la distribuzione cercando Ubuntu (o WSL) nel menù di start.

> [!CAUTION]
> Come spiegato sopra, è possibile che dopo il riavvio dall'installazione di WSL, una finestra del terminale si apra
> automaticamente per consentire le ultime operazioni di installazione. Lasciar terminare e quindi proseguire nella
> guida.

Ti verrà poi chiesto di **immettere un nome utente** e **una password**. Questi sono specifici della distribuzione di
Ubuntu installata e non hanno alcuna relazione con nome utente e password di Windows.

> [!CAUTION]
> Il nome utente inserito deve soddisfare i requisiti di Unix `NAME_REGEX="^[a-z][-a-z0-9_]*$"`. Può quindi essere
> composto solo da lettere minuscole, numeri, il carattere speciale '-' e deve iniziare con una lettera minuscola.

> [!IMPORTANT]
> Durante l'inserimento della password, per motivi di sicurezza, non vedrai i caratteri inseriti, né il movimento del
> cursore. Il sistema chiederà l'inserimento della password due volte; se le password inserite non coincidono, la
> procedura verrà ripetuta.

> [!CAUTION]
> Se dimentichi la password della distribuzione di Linux fai riferimento a
> [questa guida](https://docs.microsoft.com/it-it/windows/wsl/user-support#forgot-your-password) per recuperarla.

> [!TIP]
> Se la dimensione del font del terminale risultasse essere troppo piccola, è possibile zoomare facendo CTRL+scroll
> del mouse/trackpad.

Aggiorna quindi il catalogo pacchetti della distribuzione. Per Ubuntu è possibile farlo eseguendo il seguente comando
dal terminale:

``` bash
$ sudo apt update && sudo apt upgrade
```

> [!NOTE]
> Il comando `sudo`, usato come prefisso al comando `apt`, consente di eseguire quest'ultimo come amministratore di
> sistema (detto _root_ nel gergo Unix) e richiede l'inserimento della password utente.
> Si raccomanda di aggiornare periodicamente la distribuzione, indicativamente una volta alla settimana.

> [!TIP]
> Per verificare che l'installazione di WSL sia andata a buon fine, chiudi e riapri Ubuntu 24.04 LTS, cercando il
> programma come fai con le altre applicazioni Windows, poi digita il comando:
>
> ```bash
> $ whoami
> carlo
> ```
>
> In caso di successo, il tuo nome utente verrà stampato sul terminale.

### Installazione degli strumenti di base

Per installare ulteriori pacchetti, utilizza il comando `sudo apt install`. Ad esempio, per installare `clang-format`
e `g++`, usa il comando:

``` bash
$ sudo apt install git clang-format g++
```

> [!TIP]
>
> Per verificare la corretta installazione dei pacchetti appena descritti, eseguire i seguenti comandi:
>
> ```bash
> $ git --version
> git version 2.43.0
> ```
>
> ```bash
> $ g++ --version
> g++ (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
> Copyright (C) 2023 Free Software Foundation, Inc.
> This is free software; see the source for copying conditions.  There is NO
> warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
> ```
>
> ```bash
> $ clang-format --version
> clang-format version 18.1.3
> ```
>
> I numeri di versione riportati sopra sono solo indicativi, e possono variare nel tempo, **quello che è importante**
> è che **nessuno dei tentativi** di esecuzione **termini con un errore del tipo** `Command 'git/g++/clang-format' not
> found`.

## Installazione di Visual Studio Code

Il WSL è pensato per essere usato soprattutto da linea di comando all'interno di un terminale testuale. E' quindi
possibile eseguire agevolmente ad esempio la compilazione di un programma con `g++` o la formattazione del suo codice
sorgente con `clang-format`.

Però, per chi non ha troppa familiarità con il terminale, altre azioni sono invece meno agevoli, prima fra tutte la
possibilità di modificare file. Editor testuali, quali `nano`, `vim` e `emacs`, sono certamente disponibili (dopo
un'eventuale installazione), ma esiste anche la possibilità di editare file direttamente da Windows, usando editor come
Visual Studio Code (VS Code).

> [!IMPORTANT]
> Prima di iniziare, assicurati di aver completato l'installazione di WSL.

In primo luogo, **scarica e installa** [VS Code](https://code.visualstudio.com/) **su Windows**.

Durante l'installazione assicurati di selezionare l'opzione "Add to PATH" così da poter aprire VS Code con il comando
`code` da terminale. Al termine riavvia il PC.

> [!CAUTION]
> **NON** installare VS Code nella distribuzione Linux in ambiente WSL.

A questo punto, installa l'estensione **Visual Studio Code Remote - WSL**, che permette di usare WSL come ambiente di
sviluppo direttamente da VS Code.

Per farlo, apri il
[seguente link](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
e procedi.

### Aprire una cartella remota

Una volta configurato VS Code, sarà possibile aprire una cartella interna a WSL direttamente in VS Code.

1. Per prima cosa apri WSL (selezionando Ubuntu nel menù di start o lanciando `wsl` da Powershell)

2. Esegui il comando `code .` da terminale.

Dopo qualche istante si aprirà una nuova finestra di VS Code, ed eseguirà l'installazione e la configurazione
automaticamente. Una volta completato apparirà un nuovo indicatore nell'angolo in basso a sinistra, indicando la
riuscita dell'operazione.

_Potrebbe apparire un messaggio di conferma di affidabilità della cartella da cui si è
eseguito il comando `code .`, in tal caso premere "Si."_

![WSL indicator in VS Code](https://code.visualstudio.com/assets/docs/remote/wsl/wsl-statusbar-indicator.png)

> [!TIP]
> Puoi leggere la [documentazione ufficiale](https://code.visualstudio.com/docs/remote/wsl) per ulteriori dettagli.

## Verificare il funzionamento dell'interfaccia grafica

Da Powershell, aperta con permessi da amministratore, esegui il seguente comando:

```powershell
> wsl --update
```

In seguito, per verificare se la versione di WSL installata supporta l'interfaccia grafica, da Ubuntu, installa le
applicazioni di esempio con il comando:

```bash
$ sudo apt install x11-apps
```

e prova ad aprire una finestra grafica che visualizza l'ora corrente tramite il comando:

```bash
$ xclock
```

Se si apre una finestra come la seguente, l'installazione ha avuto successo.

![XClock](images/xclock.jpg)

In caso contrario, si rimanda a [questa guida](XSrvGuide.md), per l'installazione di programmi aggiuntivi.

## Risoluzione dei problemi

### Fallimento nella creazione dello user su Ubuntu

Se all'avvio di WSL il prompt è simile a:

```bash
root@LAPTOP:~$
```

indicando root come nome utente, vuol dire che l'utente di default non è stato configurato correttamente.

Per risolvere, aprire Powershell come amministratore e eseguire il comando:

```powershell
> ubuntu2024.exe config --default-user <USERNAME>
```

> [!NOTE]
> Può essere necessario variare il comando in base alla distribuzione di linux installata (i.e. `ubuntu-2204.exe`). Si
> suggerisce di sfruttare il completamento automatico per individuare il comando corretto, digitando per esempio
> `ubuntu` seguito dal tasto ⇆ (tab).
>
> Il nome utente  DEVE essere quello indicato in fase di installazione. Nel caso in cui non ci si ricordasse il nome
> utente, è possibile leggere l'elenco degli utenti con: `cat /etc/passwd`. Il proprio utente sarà tra gli ultimi
> presenti nella lista.

### Reset della password in Ubuntu

Per resettare la propria password su Ubuntu, qualora venga dimenticata, aprire Powershell come amministratore ed
eseguire il comando:

```powershell
> wsl -u root
```

che dovrebbe permettervi di accedere a Ubuntu come utente `root`.

A questo punto digitare il comando indicato sotto e digitare (due volte), la nuova password che si intende utilizzare
per il proprio utente:

```bash
root@LAPTOP:~$ passwd <USERNAME>
New password: 
Retype new password: 
```

> [!NOTE]
> Durante la digitazione della password non noterete alcuno spostamento del cursore.
> La cosa è perfettamente normale.

### sudo apt update fallisce "Temporary failure resolving 'archive.ubuntu.com'"

Il problema può essere causato da una cattiva configurazione di rete.

Una soluzione può essere il ripristino delle impostazioni di DNS di windows.

Avviare Powershell come amministratore, ed eseguire i seguenti comandi:

```powershell
> netsh winsock reset 
> netsh int ip reset all
> netsh winhttp reset proxy
> ipconfig /flushdns
```

Riavviare in seguito il dispositivo.

### Impossibile avviare la macchina virtuale perché una funzionalità richiesta non è installata

Il problema può essere causato dalla disattivazione a livello di BIOS della Virtualizzazione sulla prossima macchina.

Si può verificare il problema verificando lo stato della `Virtualizzazione` nella scheda `Prestazioni` di
`Gestione attività`.

> [!TIP]
> Usando la combinazione di tasti <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Esc</kbd> è possibile aprire rapidamente
> Gestione Attività. Se la scheda non è visibile cliccare su `Più dettagli`.

Se Virtualizzazione è indicato come disabilitato è necessario abilitarlo da BIOS.

### Impossibile avviare VSCode su WSL con il comando `code`

VSCode server è impostato erroneamente, chiudere WSL e VSCode.

Da Powershell ed eseguire il seguente comando:

```powershell
> wsl.exe --shutdown
```

Dopodiché riavviare VSCode **da Windows** e aprire una nuova finestra su WSL cliccando sul bottone verde in basso a
sinistra e selezionando "Connect to WSL" dal menù a tendina.

### Passare file tra Windows e WSL

#### Accedere a Windows file system da WSL

Da WSL è possibile accedere ai file presenti sulla propria macchina Windows tramite un Mount point.

Per farlo è sufficiente navigare su `/mnt/<Drive>` sostituendo a `<Drive>` la lettera corrispondente al disco da
raggiungere.

Per esempio, per navigare nel disco `C:\` il comando da lanciare su WSL è:

```bash
$ cd /mnt/C/
```

A questo punto possono essere utili i comandi `cp` o `mv` per trasferire i file da e su WSL.

> [!CAUTION]
> Si raccomanda la massima attenzione quando si naviga nelle cartelle di sistema, per evitare di causare danni al
> sistema operativo Windows.

#### Accedere al filesystem Linux da Windows

Il filesystem Linux è salvato in una posizione nascosta e non facilmente raggiungibile del sistema PER BUONE RAGIONI.

Il metodo di accesso ai file di un sistema NT (come Windows) è differente rispetto a sistemi Unix (come Linux) e
accedere direttamente ai file salvati sulla distribuzione Linux da Windows causerebbe certamente danni al file stesso o
peggio all'intero filesystem.

Per poter accedere/creare/modificare file presenti nel filesystem della distribuzione Linux da tool e applicazioni
Windows, bisogna necessariamente passare da un Mount point.

Questo si trova in `\\wsl$\<Distro>` con `<Distro>` che corrisponde al nome della distribuzione di Linux scelta, che si
può trovare come descritto nella sezione ['Cambiare la versione di WSL'](#cambiare-la-versione-di-wsl).

Per esempio, con una distribuzione Ubuntu, si può navigare nelle cartelle Linux semplicemente inserendo nella Barra
degli Indirizzi di Esplora Risorse `\\wsl$\Ubuntu\` e da lì accedere alla propria home utente.

In alternativa è sufficiente lanciare il comando `explorer.exe` dalla bash di WSL, specificando in argomento la cartella
in cui navigare.

```bash
$ explorer.exe /home/user/
```

Per esempio il comando sopra aprirà Esplora Risorse nella cartella home dell'utente user.

> [!TIP]
> Si può passare l'argomento `.`(punto) per aprire Esplora Risorse nella cartella WSL aperta in quel momento dalla
> command line:
>
> ```bash
> $ explorer.exe .
> ```
>

A questo punto è possibile operare sui file in maniera usuale.

### Cambiare la versione di WSL

Nel caso in cui sia già stata installata una distribuzione Linux e vi sia intenzione di cambiare la versione di WSL per
la specifica distribuzione, è possibile farlo da Powershell.

Aprire Powershell come amministratore.

Copiare ed eseguire il seguente comando:

``` Powershell
> wsl -l -v
```

per visualizzare la lista delle distribuzioni Linux installate sulla macchina e la versione di WSL in uso per ciascuna.

Eseguire il seguente comando:

``` Powershell
> wsl --set-version <DISTRO> <VERSION>
```

sostituendo `<Distro>` (compresi `<` e `>`) con il nome della distribuzione da modificare, come visualizzato nella lista
precedente, e `<Version>` con 1 se si vuole passare a WSL 1 o 2 se si vuole passare a WSL 2.

Per esempio, se avessimo installato una distribuzione Ubuntu con WSL 1 e volessimo aggiornare a WSL 2 il comando da
lanciare sarebbe:

``` Powershell
> wsl --set-version Ubuntu 2
```

> [!NOTE]
> Si ricorda che per poter aggiornare a WSL 2 è necessario aver attivato la funzionalità aggiuntiva "Virtual Machine
> Platform" come spiegato nel punto 1 della guida.

### Aggiornare la distribuzione di Ubuntu

Se in seguito all'installazione, la versione di Ubuntu installata non è la più recente, è possibile aggiornarla da linea
di comando.

Per verificare la versione installata eseguire il seguente comando da WSL:

```bash
$ cat /etc/os-release
```

Se `VERSION_ID` non è minore di 24.04 è possibile aggiornare con il seguente comando:

```bash
$ sudo do-release-upgrade
```
