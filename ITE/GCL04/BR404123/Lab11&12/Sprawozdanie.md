
# Projekt 
## Rosiak B�a�ej
### Wdra�anie na zarz�dzalne kontenery: Kubernetes
Instalacja minikube'a:

![](1.png)

Uruchomienie minikube'a i dashboarda:

![](2.png)
![](3.png)

Kontener minikube'a:

![](4.png)

Utworzenia poda nginx:

![](5.png)
![](6.png)

Przekierowanie port�w + sprawdzenie poprawno�ci dzia�ania:

![](7.png)
![](8.png)

Utworzenie YAML'a tworz�cego dwa pody *nginx*, stworzenie pod�w na podstawie plik�w i sprawdzenie dzia�ania:

![](9.png)
![](10.png)
![](11.png)

Zmiana ilo�ci replik/pod�w na 4 (zmiana, wdro�enie i sprawdzenie):

![](12.png)
![](13.png)
![](14.png)

Badanie stanu za pomoc� *kubectl rollout status*:

![](15.png)

Budowa obrazu, kt�re zadaniem b�dzie zawsze zwr�ci� b��d:

![](16.png)
![](17.png)

Zabawa podami (ilo�ci� replik):
- 8 replik:

![](18.png)
![](19.png)

- 1 replika:

![](20.png)
![](21.png)

- 0 replik:

![](22.png)
![](23.png)

- Nowsza wersja:

![](24.png)
![](25.png)

- Z�y obraz:

![](26.png)
![](27.png)

U�ycie komendy *kubectl rollout history* w celu pokazania historii zmian oraz *kubectl rollout undo* w celu wycofania ostatniego, niedzia�aj�cego kontenera:

![](28.png)

Utworzenie skryptu weryfikuj�cego czy wdro�enie zd��y�o si� wdro�y� i uruchomienie go:

![](29.png)