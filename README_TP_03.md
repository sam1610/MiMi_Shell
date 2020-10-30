# TP_03

All questions wil be  deleted at the end of each exercice. 

## Exercice 1
Pour commencer, vous allez récupérer les données nécessaires à l’ensemble des exercices. 
Placez-vous dans le répertoire correspondant à ce TP pour y extraire l’archive après l’avoir chargée à l’URL suivante : 
http ://julien.sopena.fr/LU2IN020-TP_03.tgz

Yes, take the link put open it in the directory called TP3

### Question 1
!wget http://julien.sopena.fr/LU2IN020-TP_03.tgz
!tar  -xvzf LU2IN020-TP_02.tgz

ls
exo1/  exo2/  exo3/


### Question 2
Ouvrez le fichier cesar.c contenu dans le répertoire exo1 et étudiez-le. Que fait-il ?

cat cesar.c
```c
#include<stdlib.h>
#include<stdio.h>
 
int main(int argc, char const *argv[])
{
char c;
int cle;
 
if (argc != 2) {
fprintf(stderr, "Il faut donner une cle\n");
fprintf(stderr, "Usage : %s <un_entier>\n", argv[0]);
exit(1);
}
 
cle = atoi(argv[1]);
while (EOF != (c = fgetc(stdin)))
if ('a' <= c && c <= 'z')
printf("%c", 'a' + (c - 'a' + cle) % 26);
else
printf("%c", c);
 
return 0;
}
```

Le programme verifie l'existance d’un paramètre au niveau de la structure conditionnelle et arrête l'exécution si le paramètre manque. 
Sinon, le programme lira le contenu d’une chaine, caractère par caractère et vérifie si chaque caractère est un alphabet minuscule, ensuite il effectue un décalage d’un certain nombre de  places défini par la variable "cle" qui est l'argument  passe lors de l execution du programme, 
( il will  update the content later, .  have alook at   what i sent n whatsapp)



### Question 3

Testez-le après l’avoir compilé. Pour quitter le programme, il faut simuler une fin de fichier en combinant les touches Ctrl+d.
gcc    cesar  
./cesar  1


abcd
Output :   bcde
Papa in the readme file, put the execution you did with the parameter and show the output you got in the console.
Yes i will,  , you mean  drop th image?  Or just right what I got ?

###Question 4
Le répertoire fenetre_sur_coquillage contient un texte chiffré par décalage, puis fragmenté en plu- sieurs fichiers. En essayant tous les décalages possibles sur le premier fragment part1, trouvez la clé de déchiffrement.
```shell
cat  part1  |   ../cesar 16
```
- output
>  Lo Bkcr m'ocd wêwo cyec Wsxnygc !!!
Le Bash c'est même sous Windows !!!


>  la cle = 16

### Question 5
Maintenant que vous avez récupéré la clé, utilisez-la pour déchiffrer l’ensemble des fichiers et concaténez les résultats dans un même fichier news.txt qui contiendra tout le texte en clair.
```shell
for i in {1..9}; 
do 
 cat ./fenetre_sur_coquillage/part"$i" |  ../cesar 16  >> news.txt; 
done
```

 output 
  Le Bash c'est même sous Windows !!!
Grâce à Windows Subsystem for Linux (wsl),
Le Bash c'est même sous Windows !!!
Grâce à Windows Subsystem for Linux (wsl),
il est aujourd'hui possible d'exécuter des
exécutables binaires Linux (au format ELF)
de manière native sur Windows 10. On peut
voir ce mécanisme comme une émulation du 
"mode user" d'un système gnu-Linux. Une fois
activé, on a accès à plusieurs distributions
intégrant Bash.


Une autre solution :
```shell
 for i in ./fenetre_sur_coquillage/part*;
do
  ./cesar 16 < $i  >>  news.txt;
done
```




## Exercice 2
  SplitStrip
  
  ### Question 1
```shell
#!/bin/bash
Folder="Data";
if [ ! -d $Folder ]; then
   mkdir $Folder;
fi

for  i in {00..99};do
 if [ ! -f $Folder/data."$i" ]; then
     wget  http://julien.sopena.fr/chunks/data."$i"  -P ./Data ||          break; 
 fi
done;
```
  
  ### Question 2
  > concatiner tous les fichier  data.xx au sein d'un seul fichier  result
  ```shell
  #!bin/bash
for i in ./Data/data*; do
 cat $i >> ./Data/result;
done
```
  
 ### Question 3
 
 > Afficher le type du fichier binaire
 ```shell 
  file result
```
  - output: 
  result: JPEG image data, Exif standard: [TIFF image data, little-endian, direntries=0], baseline, precision 8, 650x897, components 3

  > renommer lte fichier
  
  ```shell 
  mv result  image.jpg
```
## Exercice 3
### Qyestion 1
commande proposée
```shell
 wc -c < fichier
```
// Afficher le nombre de caractère du fichier test
```shell
 wc -c < test
```
-Affiche: 42



### Question 2
>  Afficher le plus gros fichier du repertoir, 

```shell
#!/bin/bash
# Vérificaiton de l'exisytance du  nom du dossier comme paramètre
if [ -z  $1 ] ; then
  echo " pas de paramètre fourni"; exit -1;
else
# vérification de l'existance du dossie précisé au niveau du paramètre
   if  [  ! -d  $1 ]; then
        echo  "  le dossier   $1  n'exixte pas "; exit -1;
   else
   #  retenir seulement le fichier le plus Gros et afficher son nom
         echo "Le plus gros fichier est : " $(find $1/ -type f -printf "%s %p\n" | sort -rn >
   fi

fi

```
>  execution  :
- $ bash   biggest.sh    ./dd
  le dossier   ./dd  n'exixte pas
- $ bash   biggest.sh
 pas de paramètre fourni

- $ bash   biggest.sh    ./dico
Le plus gros fichier est :  185 ./dico/bien
