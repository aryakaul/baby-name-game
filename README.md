# Rank guesses for a baby name!

Do you have a friend who is having a baby? Are the friends of that friend interested in guessing the name of the future child? Are the friends of that friend interested in having a logical alignment-based score to see whose guess was the closest to the actual baby name?

You are in luck!

This script first reads all names on Social Security applications from 1980-2022 and generates a co-occurrence matrix for each character. We deem this substitution matrix NAMELY62. 

It then calculates the Needleman-Wunsch alignment of each person's guess to the real baby name and computes a score for each guessed name. The winner is outputted at the end!

```
$ ./baby-name-game -h
usage: baby-name-game [-h] [-n NAMES] [-v] [-r REALNAME] [-f GUESSEDNAMES]

Rank a list of guessed baby names to the one true baby name.

optional arguments:
  -h, --help            show this help message and exit
  -n NAMES, --names NAMES
                        Baby names from Social Security Card applications in the US from 1880-2022. Downloaded from: https://catalog.data.gov/dataset/baby-names-from-social-security-card-applications-national-data
  -v, --verbose         Increase verbosity level.
  -r REALNAME, --realname REALNAME
                        Real name of the baby. Default is Alice
  -f GUESSEDNAMES, --guessednames GUESSEDNAMES
                        CSV file of guessed names. First entry is person who submitted name. Second entry is the guessed name.
```

For example, if the real name is "Alice":
```
$ cat ./guessednames
Arya,Alicia
Bob,Tomato
Timothy,Boop
$ ./baby-name-game -n ./allnames.csv -r Alice -f ./guessednames
INFO     | __main__:main:184 - Creating NAMELY62 scoring matrix...
INFO     | __main__:main:194 - Created NAMELY62 scoring matrix.
INFO     | __main__:main:196 - Actual name is Alice
INFO     | __main__:main:206 - Performing Needleman-Wunsch alignment for guessed names...
INFO     | __main__:main:215 - 
    Arya guessed Alicia with a score of 1.772589342069186.
    Alic-e
    Alicia
INFO     | __main__:main:215 - 
    Bob guessed Tomato with a score of -0.9999974474071582.
    Alice-
    Tomato
INFO     | __main__:main:215 - 
    Timothy guessed Boop with a score of -0.9999977696690966.
    Alice
    Boo-p
SUCCESS  | __main__:main:217 - Winner is Arya!
```

There are better ways to do this, I cobbled this together very quickly. If you have suggestions make a PR! 
