# Zaj�cia 09
### 2022-05-04 -- 2022-05-06
---
# Przygotowanie wdro�e� nienadzorowanych dla platform z pe�nym OS

## Zadania do wykonania
### Przygotowanie systemu pod uruchomienie
* Przeprowad� instalacj� systemu Fedora w VM, skonfiguruj u�ytkownik�w (u�yj hase�, kt�re mo�na bezkarnie umie�ci� na GitHubie!), sie�, wybierz podstawowy zbi�r oprogramowania, optymalnie bez GUI
- ![image](screens/1.PNG "install")
- ![image](screens/2.PNG "install")
- ![image](screens/3.PNG "install")
Instalacja uruchomienie serwera ssh oraz przerzucenie pliku przez WINSCP do edycji
* Przeprowad� drug� instalacj� systemu Fedora w VM - celem drugiego systemu b�dzie wy��cznie serwowanie repozytorium przez HTTP
- ![image](screens/4.PNG "install")
- ![image](screens/5.PNG "install")
Pobranie pliku oraz zedytowanie go aby przeprowadza� instalacj� tekstow� z odpowiedniego repo
- ![image](screens/6.PNG "install")
- ![image](screens/7.PNG "install")
W trakcie instalacji potrzebne by�o wci�ni�cie ESC i wpisanie komendy: linux inst.ks=https://raw.githubusercontent.com/InzynieriaOprogramowaniaAGH/MDO2022_S/PK400223/ITE/GCL04/PK400223/Lab09/ksfile.ks
aby instalacja z pliku z serwera http si� uda�a

