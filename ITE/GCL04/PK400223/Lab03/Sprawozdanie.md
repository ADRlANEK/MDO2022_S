# Zaj�cia 03
### 2022-03-21 -- 2022-03-25
---
# Docker files, kontener jako definicja etapu

### Przeprowadzenie buildu w kontenerze
1. Wykonaj kroki build i test wewn�trz wybranego kontenera bazowego. Tj. wybierz "wystarczaj�cy" kontener, np ```ubuntu``` dla aplikacji C lub ```node``` dla Node.js
	* uruchom kontener
	* pod��cz do niego TTY celem rozpocz�cia interaktywnej pracy
	* ```docker run -it node:14-alpine3.15 sh ```
	 - ![image](screens/1.PNG "run")
	* zaopatrz kontener w wymagania wst�pne (je�eli proces budowania nie robi tego sam)
	* ```apk add git```
	* ![image](screens/2.PNG "git add")
	* sklonuj repozytorium
	* ``` git clone https://github.com/gothinkster/vue-realworld-example-app ```
	* ![image](screens/3.PNG "git clone")
	* uruchom build
	* ```npm install```
	* ```npm run build```
	* ![image](screens/4.PNG "build")
	* ![image](screens/5.PNG "build")
	* uruchom testy
	* ```npm test```
	* ![image](screens/6.PNG "test")
	* ![image](screens/7.PNG "test")
2. Stw�rz dwa pliki Dockerfile automatyzuj�ce kroki powy�ej, z uwzgl�dnieniem nast�puj�cych kwestii
	* Kontener pierwszy ma przeprowadza� wszystkie kroki a� do builda
	* ``` docker build -f Docker-builder . ```
	* ![image](screens/8.PNG "builder")
	* ![image](screens/9.PNG "builder")
```bash
FROM node:14-alpine3.15
WORKDIR ./
RUN apk add git
RUN apk add python2
RUN git clone https://github.com/gothinkster/vue-realworld-example-app.git
WORKDIR /vue-realworld-example-app
RUN npm install
RUN npm build
```
* Kontener drugi ma bazowa� na pierwszym i wykonywa� testy
* ``` docker build -f Docker-runner . ```
```bash
FROM 5a09bc57cc62
CMD ["npm", "test"]
```
3. Wyka�, �e kontener wdra�a si� i pracuje poprawnie. Pami�taj o r�nicy mi�dzy obrazem a kontenerem. Co pracuje w takim kontenerze?

``` docker run #value of image id ```

![image](screens/10.PNG "runner")
![image](screens/11.PNG "runner")