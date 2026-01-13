# Level 01

## Objectif
L'objectif est de se connecter en tant qu'utilisateur `flag01` pour exécuter la commande `getflag`.

## Analyse
En regardant dans le dossier courant, il n'y a rien de particulier.
Cependant, on peut vérifier le fichier `/etc/passwd` qui contient les informations des utilisateurs. Sur les vieux systèmes ou les systèmes mal configurés, les hashs des mots de passe peuvent s'y trouver (au lieu de `/etc/shadow`).

```bash
cat /etc/passwd | grep flag01
```

On obtient une ligne intéressante :
`flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash`

Le hash du mot de passe est `42hDRfypTqqnw`.

## Exploitation
Il faut cracker ce hash. On peut utiliser un outil comme **John the Ripper**.

1.  Créer un fichier contenant le hash (sur sa machine locale ou dans `/tmp` si on a les droits d'écriture et l'outil).
    ```bash
    echo "42hDRfypTqqnw" > hash.txt
    ```

2.  Lancer John the Ripper :
    ```bash
    john hash.txt
    ```
    
    *Output attendu :*
    ```
    Loaded 1 password hash (descrypt, traditional crypt(3) [DES 128/128 AVX-512])
    abcdefg          (?)
    ```

Le mot de passe trouvé est `abcdefg`.

## Résolution
On se connecte avec l'utilisateur `flag01` et on récupère le flag.

```bash
su flag01
# Password: abcdefg
getflag
```

**Token**: f2av5il02puano7naaf6adaaf
