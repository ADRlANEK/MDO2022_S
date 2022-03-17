# Zaj�cia 02
### Przemys�aw Kudriawcew
---
## Zadania do wykonania
1. Przygotuj git hook, kt�ry rozwi��e najcz�stsze problemy z commitami
* hook sprawdzaj�cy, czy tytu� commita nazywa si� ```<inicja�y><numer indeksu>```
* hook sprawdzaj�cy, czy w tre�ci commita pada numer labu, w�a�ciwy dla zadania
- ![image](screens/1.PNG "hook")
2. Umie�� hook w sprawozdaniu w taki spos�b, aby da�o si� go przejrze�
W pliku commit-msg zamieszczono poni�szy skrypt
``` #!/usr/bin/env bash```
```INPUT_FILE=$1```
```START_LINE=`head -n1 $INPUT_FILE` ```
```PATTERN="^(PK400223)"```
```PATTERN2=".*(Lab)[0-9][0-9]*."```
```if ! [[ "$START_LINE" =~ $PATTERN ]]; then```
  ```echo "Bad commit title, see example: 400223: message"```
  ```exit 1```
```fi```
```while IFS= read -r line```
```do```	
	```if [[ $line =~ $PATTERN2 ]]; then```
		```exit 0```
	```fi```
```done < <(sed 1d $INPUT_FILE)```
```echo "Bad commit message, needs to contain Lab0X or LabXX number according to actual lab number"```
```exit 1 ```
3. Rozpocznij przygotowanie �rodowiska Dockerowego
    * zapewnij dost�p do maszyny wirtualnej przez zdalny terminal (nie "przez okienko")
    * - ![image](screens/2.PNG "ssh")
    * je�eli nie jest stosowane VM (np. WSL, Mac, natywny linux), wyka� ten fakt **dok�adnie**
    * zainstaluj �rodowisko dockerowe w stosowanym systemie operacyjnym
4. Dzia�anie �rodowiska
    * wyka�, �e �rodowisko dockerowe jest uruchomione i dzia�a (z definicji)
    * - ![image](screens/3.PNG "dockerd")
    * wyka� dzia�anie z spos�b praktyczny (z w�asno�ci):
      * pobierz obraz dystrybucji linuksowej i uruchom go
      * - ![image](screens/4.PNG "pull")
      * wy�wietl jego numer wersji
      * - ![image](screens/5.PNG "image")
5. Za�� konto na Docker Hub
- ![image](screens/6.PNG "dhub")
-  ![image](screens/7.PNG "dhub")