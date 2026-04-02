# Installazione del pacchetto di analisi [ROOT](https://root.cern/) (OPZIONALE)

- [Installazione del pacchetto di analisi ROOT (OPZIONALE)](#installazione-del-pacchetto-di-analisi-root-opzionale)
  - [Installazione su Ubuntu (o Windows con WSL)](#installazione-su-ubuntu-o-windows-con-wsl)
  - [Installazione in macOS](#installazione-in-macos)
  - [Risoluzione dei problemi](#risoluzione-dei-problemi)
    - [Mismatch tra la versione del compilatore e del pacchetto ROOT (macOS)](#mismatch-tra-la-versione-del-compilatore-e-del-pacchetto-root-macos)

## Installazione su Ubuntu (o Windows con WSL)

La strategia suggerita è quella di **installare una versione precompilata** di ROOT, fornita dagli sviluppatori del
pacchetto di analisi.

Per farlo, devi però installare in anticipo alcune _dipendenze_ necessarie per il funzionamento del programma:

```bash
$ sudo apt install binutils cmake dpkg-dev g++ gcc libssl-dev git libx11-dev \
libxext-dev libxft-dev libxpm-dev python3 libtbb-dev libvdt-dev libgif-dev
```

Così come alcuni pacchetti, non strettamente necessari, ma fortemente consigliati:

```bash
$ sudo apt install gfortran libpcre3-dev \
libglu1-mesa-dev libglew-dev libftgl-dev \
libfftw3-dev libcfitsio-dev libgraphviz-dev \
libavahi-compat-libdnssd-dev libldap2-dev \
 python3-dev python3-numpy libxml2-dev libkrb5-dev \
libgsl-dev qtwebengine5-dev nlohmann-json3-dev libmysqlclient-dev \
libgl2ps-dev \
liblzma-dev libxxhash-dev liblz4-dev libzstd-dev
```

> [!WARNING]
> La lista delle dipendenze potrebbe cambiare nel tempo, seguendo l'evoluzione di ROOT e della distribuzione Ubuntu.
>
> In caso i comandi presentati non risultino corretti, consulta
> [questa pagina](https://root.cern/install/dependencies/).

A questo punto, scarica i binari precompilati di ROOT al
[link sulla pagina ufficiale del pacchetto](https://root.cern/install/all_releases/).

Cliccando sulla **latest stable** vedrai che esistono diverse versioni di pacchetti precompilati corrispondenti a
diversi sistemi operativi.

> [!IMPORTANT]
> Verifica, da Ubuntu, la versione del sistema operativo installato tramite il comando
>
> ```bash
> $ lsb_release -a
> ```

Per iniziare il download di ROOT copia quindi _il link_in blu corrispondente al tuo sistema operativo (es:
`https://root.cern/download/root_v6.36.04.Linux-ubuntu24.04-x86_64-gcc13.3.tar.gz`) ed esegui i comandi:

```bash
$ cd
$ wget https://root.cern/download/root_v6.36.04.Linux-ubuntu24.04-x86_64-gcc13.3.tar.gz

--2024-09-18 21:42:05--  https://root.cern/download/root_v6.36.04.Linux-ubuntu24.04-x86_64-gcc13.3.tar.gz
...
```

Una volta completato il download, esegui l comando:

```bash
tar -xzvf root_v6.36.04.Linux-ubuntu24.04-x86_64-gcc13.3.tar.gz
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
>  | Welcome to ROOT 6.36.04                        https://root.cern |
>  | (c) 1995-2025, The ROOT Team; conception: R. Brun, F. Rademakers |
>  | Built for linuxx8664gcc on Aug 25 2025, 00:00:00                 |
>  | From tags/6-36-04@6-36-04                                        |
>  | With g++ (GCC) 11.5.0 20240719 (Red Hat 11.5.0-5)                |
>  | Try '.help'/'.?', '.demo', '.license', '.credits', '.quit'/'.q'  |
>   ------------------------------------------------------------------
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
>  | Welcome to ROOT 6.36.04                        https://root.cern |
>  | (c) 1995-2025, The ROOT Team; conception: R. Brun, F. Rademakers |
>  | Built for macosxarm64 on Aug 25 2025, 09:02:18                   |
>  | From tags/6-36-04@6-36-04                                        |
>  | With Apple clang version 17.0.0 (clang-1700.0.13.3)              |
>  | Try '.help'/'.?', '.demo', '.license', '.credits', '.quit'/'.q'  |
>   ------------------------------------------------------------------
> 
> root [0] 
> ```
>
> se l'installazione ha avuto successo, puoi uscire da ROOT digitando `.q` e premendo INVIO.

## Risoluzione dei problemi

### Mismatch tra la versione del compilatore e del pacchetto ROOT (macOS)

Qualora, eseguendo `root` su macOS a seguito di un aggiornamento del sistema operativo o di _Xcode_, tu incorra in un
errore simile a:

```zsh
% root
/opt/homebrew/Cellar/root/6.38.04/etc/root/cling/std_darwin.modulemap:73:64: error: header '__type_traits/add_lvalue_reference.h' not found
    module add_lvalue_reference                       { header "__type_traits/add_lvalue_reference.h" }
                                                               ^
input_line_1:1:10: note: submodule of top-level module 'std' implicitly imported here
#include <new>
         ^
Warning in cling::IncrementalParser::CheckABICompatibility():
  Failed to extract C++ standard library version.
Warning in cling::IncrementalParser::CheckABICompatibility():
  Possible C++ standard library mismatch, compiled with _LIBCPP_ABI_VERSION '1'
  Extraction of runtime standard library version was: ''
   ------------------------------------------------------------------
  | Welcome to ROOT 6.38.04                        https://root.cern |
  | (c) 1995-2025, The ROOT Team; conception: R. Brun, F. Rademakers |
  | Built for macosxarm64 on Mar 11 2026, 21:39:24                   |
  | From tags/6-38-04@6-38-04                                        |
  | With Apple clang version 17.0.0 (clang-1700.6.4.2) std201703     |
  | Try '.help'/'.?', '.demo', '.license', '.credits', '.quit'/'.q'  |
   ------------------------------------------------------------------
```

puoi provare a reinstallare ROOT tramite `brew`, ricompilandolo:

```zsh
% brew reinstall -s root
Warning: building from source is not supported!
You're on your own. Failures are expected so don't create any issues, please!
==> Fetching downloads for: root
✔︎ API Source root.rb                                                                                                                  Verified      6.9KB/  6.9KB
✔︎ Formula root (6.38.04)                                                                                                              Verified    386.7MB/386.7MB
==> Reinstalling root 
==> cmake -S . -B builddir -DCLING_CXX_PATH=clang++ -DCMAKE_CXX_STANDARD=17 -DCMAKE_INSTALL_ELISPDIR=/opt/homebrew/Cellar/root/6.38.04/share/emacs/site-lisp/root
==> cmake --build builddir
==> ctest -R tutorial-tree --verbose --parallel 10 --test-dir builddir
==> cmake --install builddir
==> Caveats
[...]
```

> [!WARNING]
> Non è assicurato che il processo di ricompilazione funzioni.
> Tenta questa opzione solo se non ce ne sono altre e **consultati coi docenti** prima di eseguirla.

> [!NOTE]
> In questo caso il problema è dovuto al fatto che [la versione precompilata](https://root.cern/releases/release-63610/)
> di ROOT sia stata generata utilizzando una versione del compilatore meno recente di quella installata tramite
> l'aggiornamento di macOS.
