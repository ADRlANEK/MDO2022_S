# Zaj�cia 01 - Grupa 4
### Przemys�aw Kudriawcew 
---
## Zadania do wykonania
1. Zainstaluj klienta Git i obs�ug� kluczy SSH
 - ![image](screens/1.PNG "instalation")
2. Sklonuj repozytorium https://github.com/InzynieriaOprogramowaniaAGH/MDO2022_S za pomoc� HTTPS
 - ```git clone https://github.com/InzynieriaOprogramowaniaAGH/MDO2022_S.git```
 - ![image](./screens/2.PNG "https gh")
3. Upewnij si� w kwestii dost�pu do repozytorium jako uczestnik i sklonuj je za pomoc� utworzonego klucza SSH
   - Utw�rz dwa klucze SSH, inne ni� RSA, w tym co najmniej jeden zabezpieczony has�em
   - ```ssh-keygen -t ed25519```
   - ![image](screens/3.PNG "key1")
   - Skonfiguruj klucz SSH jako metod� dost�pu do GitHuba
   - ![image](screens/4.PNG "key2")
   - Sklonuj repozytorium z wykorzystaniem protoko�u SSH
   - ```git clone git@github.com:InzynieriaOprogramowaniaAGH/MDO2022_S.git```
   - ![image](screens/5.PNG "key3")
4. Prze��cz si� na ga��� ```main```, a potem na ga��� swojej grupy (pilnuj ga��zi i katalogu!) 
 - ```git checkout main```
 - ```git checkout ITE-GCL04```
 - ![image](screens/6.PNG "mainbranch")
5. Utw�rz ga��� o nazwie "inicja�y & nr indeksu" np. ```KD232144```. Miej na uwadze, �e odga��ziasz si� od brancha grupy!
 - ```git checkout -b PK400223```
 - ![image](screens/7.PNG "PK400223")
6. Rozpocznij prac� na nowej ga��zi
   - W katalogu w�a�ciwym dla grupy utw�rz nowy katalog, tak�e o nazwie "inicja�y & nr indeksu" np. ```KD232144```
   - ```mkdir PK400223```
   - W nim tak�e utw�rz katalog: Lab01
   - ```mkdir PK400223/Lab01```
   - W nowym katalogu dodaj plik ze sprawozdaniem
   - ```touch PK400223/Lab01/Sprawozdanie.md```
   - ![image](screens/8.PNG "folderstructure")
   - Dodaj zrzuty ekranu (jako inline)
   - Wy�lij zmiany do zdalnego �r�d�a
   - ```git add .```
   - ```git commit -m 'message'```
   - ``` git push --set-upstream origin PK400223 ```
   - ![image](screens/9.PNG "push")
   - Spr�buj wci�gn�� swoj� ga��� do ga��zi grupowej
   - ![image](screens/10.PNG "PR")
   - Zaktualizuj sprawozdanie i zrzuty o ten krok i wy�lij aktualizacj� do zdalnego �r�d�a (na swojej ga��zi)
7. Wystaw Pull Request do ga��zi grupowej
8. Zg�o� zadanie (Teams assignment - je�eli dost�pne)