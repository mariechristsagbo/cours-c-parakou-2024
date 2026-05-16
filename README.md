# Exercices système en C

Ce dépôt contient de petits programmes C pour expérimenter quelques notions de programmation système POSIX: manipulation de fichiers, création de processus avec `fork`, communication par `pipe`, attente avec `wait`, et lecture non bloquante.

## Fichiers

- `fs_test.c`: écrit un texte saisi par l'utilisateur dans un fichier.
- `test_counter.c`: montre que le père et le fils ont chacun leur propre copie de la mémoire après un `fork`.
- `test_proc.c`: fait communiquer un processus fils avec son père via un pipe.
- `test_proc_nbloquant.c`: variante utilisant un pipe non bloquant avec `pipe2`.
- `test_proc_nbloquant_attente.c`: variante non bloquante avec attente active en cas de `EAGAIN`.

## Compilation

Exemple avec `cc`:

```sh
cc -Wall -Wextra -std=c11 fs_test.c -o fs_test
cc -Wall -Wextra -std=c11 test_counter.c -o test_counter
cc -Wall -Wextra -std=c11 test_proc.c -o test_proc
```

Les fichiers qui utilisent `pipe2` sont spécifiques à Linux. Sur macOS, il faut remplacer `pipe2` par `pipe` puis configurer le mode non bloquant avec `fcntl`.

## Exécution

```sh
./fs_test sortie.txt
./test_counter
./test_proc
```

Ces programmes sont principalement des supports d'apprentissage. Ils peuvent être améliorés en renforçant la gestion des erreurs, la sécurité des saisies utilisateur et l'affichage des données lues depuis les pipes.
