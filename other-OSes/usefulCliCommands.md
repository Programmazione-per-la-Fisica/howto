# Foglio riepilogativo dei comandi da Terminale

## Linea di comando

```bash
$ comando [opzioni] [argomenti]
```

- `comando`: Il comando da eseguire (e.g., `ls`, `cd`, `mkdir`)
- `opzioni`: Modificatori che cambiano il comportamento del comando (di solito preceduti da `-`)
- `arguments`: Target del comando (e.g., nomi di file o directory)

Esempio:

```bash
$ ls -l /home/user/Documents
```

## Comandi base (estratto)

| Comando      | Descrizione                                 | Esempio                        | Opzioni frequenti                |
|--------------|---------------------------------------------|--------------------------------|----------------------------------|
| `mkdir`      | Crea una nuova cartella                     | `mkdir myFolder`               | `-p` (crea cartelle genitore)    |
| `cp`         | Copia files e/o cartelle                    | `cp file.txt backup.txt`       | `-r` (ricorsivo per le cartelle) |
| `mv`         | Sposta e/o rinomina files o cartelle        | `mv vecchio.txt nuovo.txt`     |                                  |
| `touch`      | Crea un file vuoto                          | `touch notes.txt`              |                                  |
| `cd`         | Cambia la cartella corrente                 | `cd Documents`                 |                                  |
| `ls`         | Elenca files e/o cartelle                   | `ls -l`                        | `-t` (ordina per tempo), `-a` (mostra file nascosti) `-h` (dimensioni file leggibili) |
| `pwd`        | Stampa la cartella di lavoro corrente       | `pwd`                          |                                  |
| `rm`         | Rimuovi files e/o cartelle                  | `rm file.txt`                  | `-r` (ricorsivo per file e le cartelle), `-i` (richiede conferma in merito ai file e cartelle da cancellare) |
| `file`       | Determina la tipologia di un file           | `file script.sh`               |                                  |

## Percorsi (Paths)

- **Path assoluti**:  
    Il percorso completo dalla radice del filesystem (inizia sempre con `/`).
    Esempio: `/Users/username/Documents/file.txt`

- **Path relativi**:  
    Il percorso relativo alla cartella corrente (dipende da dove ti trovi, non inizia con `/`).
    Esempio: `Documents/file.txt` (se sei in `/Users/username`)

## Suggerimenti utili

- Usa `ls -a` per mostrare anche i file nascosti;
- Usa `cd ..` per salire di un livello nella gerarchia delle cartelle;
- I comandi possono essere combinati: esempio `cp file1.txt ../backup/`;
- Usa il tasto `Tab` per l'auto-completamento dei nomi di file e cartelle;
- In caso di dubbi, normalmente ogni comando ha un opzione di aiuto: `comando --help` o `man comando`;
- File e cartelle nascoste iniziano con un punto (`.`), es. `.bashrc`.