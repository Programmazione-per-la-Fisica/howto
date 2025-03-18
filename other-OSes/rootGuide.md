# Installazione del pacchetto di analisi [ROOT](https://root.cern/) (OPZIONALE)

- [Installazione del pacchetto di analisi ROOT (OPZIONALE)](#installazione-del-pacchetto-di-analisi-root-opzionale)
  - [Installazione su Ubuntu (o Windows con WSL)](#installazione-su-ubuntu-o-windows-con-wsl)
  - [Installazione in macOS](#installazione-in-macos)

## Installazione su Ubuntu (o Windows con WSL)

La strategia suggerita è quella di **installare una versione precompilata** di ROOT, fornita dagli sviluppatori del
pacchetto di analisi.

Per farlo, devi però installare in anticipo alcune _dipendenze_ necessarie per il funzionamento del programma:

```bash
$ sudo apt install binutils cmake dpkg-dev g++ gcc libssl-dev \
libx11-dev libxext-dev libxft-dev libxpm-dev python3 libtbb-dev libvdt-dev libgif-dev
```

Così come alcuni pacchetti, non strettamente necessari, ma fortemente consigliati:

```bash
$ sudo apt install gfortran libpcre3-dev \
libglu1-mesa-dev libglew-dev libftgl-dev \
libfftw3-dev libcfitsio-dev libgraphviz-dev \
libavahi-compat-libdnssd-dev libldap2-dev \
python3-dev python3-numpy libxml2-dev libkrb5-dev \
libgsl-dev qtwebengine5-dev nlohmann-json3-dev libmysqlclient-dev
```

> [!WARNING]
> La lista delle dipendenze potrebbe cambiare nel tempo, seguendo l'evoluzione di ROOT e della distribuzione Ubuntu.
>
> In caso i comandi presentati non risultino corretti, consulta
> [questa pagina](https://root.cern/install/dependencies/).

A questo punto, scarica i binari precompilati di ROOT al presente [link](https://root.cern/install/all_releases/).

Cliccando sulla **latest stable** vedrai che esistono diverse versioni di pacchetti precompilati corrispondenti a
diversi sistemi operativi.

> [!IMPORTANT]
> Verifica, da Ubuntu, la versione del sistema operativo installato tramite il comando
>
> ```bash
> $ lsb_release -a
> ```

Per iniziare il download di ROOT copia quindi _il link_in blu corrispondente al tuo sistema operativo (es:
`https://root.cern/download/root_v6.32.04.Linux-ubuntu24.04-x86_64-gcc13.2.tar.gz`) ed esegui i comandi:

```bash
$ cd
$ wget https://root.cern/download/root_v6.32.04.Linux-ubuntu24.04-x86_64-gcc13.2.tar.gz

--2024-09-18 21:42:05--  https://root.cern/download/root_v6.32.04.Linux-ubuntu24.04-x86_64-gcc13.2.tar.gz
...
```

Una volta completato il download, esegui l comando:

```bash
tar -xzvf root_v6.32.04.Linux-ubuntu24.04-x86_64-gcc13.2.tar.gz
```

> [!IMPORTANT]
> Ricorda di modificare gli argomenti del comando per riflettere il nome del file che hai scaricato.

> [!TIP]
> Eseguendo il comando:
>
> ```bash
> ls
> ```
>
> dovresti vedere che nella tua home directory è apparsa una cartella che si chiama `root`.

Per completare l'installazione, modifica il file `.bashrc`, che puoi aprire eseguendo il comando:

```bash
code $HOME/.bashrc
```

ed aggiungi, alla fine del file, questa riga:

```bash
source $HOME/root/bin/thisroot.sh
```

ricordati poi di effettuare il salvataggio delle modifiche (`CTRL` + `S`).

> [!TIP]
> Per verificare la corretta installazione di ROOT:
>
> - chiudi Ubuntu e riaprila;
> - esegui il comando
>
> ```bash
> $ root
>   ------------------------------------------------------------------
>   | Welcome to ROOT 6.30/08                        https://root.cern |
>   | (c) 1995-2024, The ROOT Team; conception: R. Brun, F. Rademakers |
>   | Built for linuxx8664gcc on Jul 23 2024, 00:00:03                 |
>   | From heads/master@tags/v6-30-08                                  |
>   | With c++ (GCC) 8.5.0 20210514 (Red Hat 8.5.0-22)                 |
>   | Try '.help'/'.?', '.demo', '.license', '.credits', '.quit'/'.q'  |
>    ------------------------------------------------------------------
> 
> root [0] 
> ```
>
> se l'installazione ha avuto successo, puoi uscire da ROOT digitando `.q` e premendo INVIO.

## Installazione in macOS

Una volta installato Homebrew, per installare ROOT, esegui il comando:

```zsh
% brew install root
```

> [!TIP]
> Per verificare l'installazione esegui il comando:
>
> ```zsh
> % root
>   ------------------------------------------------------------------
>   | Welcome to ROOT 6.30/08                        https://root.cern |
>   | (c) 1995-2024, The ROOT Team; conception: R. Brun, F. Rademakers |
>   | Built for linuxx8664gcc on Jul 23 2024, 00:00:03                 |
>   | From heads/master@tags/v6-30-08                                  |
>   | With c++ (GCC) 8.5.0 20210514 (Red Hat 8.5.0-22)                 |
>   | Try '.help'/'.?', '.demo', '.license', '.credits', '.quit'/'.q'  |
>    ------------------------------------------------------------------
> 
> root [0] 
> ```
>
> se l'installazione ha avuto successo, puoi uscire da ROOT digitando `.q` e premendo INVIO.
