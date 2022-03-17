# Sprawozdanie 02
### 14.03.2022
---
## **Podpunkt 1 i 2**

Najpierw przechodz� do ukrytego katalogu `.git`, a nast�pnie do podkatalogu `hooks`

![img1](./s1.png)

Edytuj� plik `commit-msg.sample`, tak aby skrypt w nim zawarty sprawdza� tytu� commita jest odpowiedni

![img2](./s2.png)

Zmieniam nazw� pliku z `commit-msg.sample` na `commit-msg`

![img3](./s3.png)

Dzia�anie skryptu dla niepoprawnych warto�ci:

![img4](./s4.png)

Dzia�anie skryptu dla warto�ci `PP401424`:

![img5](./s5.png)

Nast�pnie przechodz� do stworzenia drugiego skryptu, kt�rego zadaniem b�dzie sprawdzenie czy w tre�ci commita jest zawarty numer labu. Post�puje podobnie jak przy poprzednim skrypcie, ale tym razem edytuj� plik `pre-commit.sample`

![img6](./s6.png)

Zmieniam jego nazw� z `pre-commit.sample` na `pre-commit`. Nast�pnie pr�buj� zrobi� commita dla warto�ci niepoprawnej

![img7](./s7.png)

I to samo lecz tym razem dla poprawnych warto�ci

![img8](./s8.png)

---

## **Podpunkt 3**

W celu wykazania pracy poprzez ssh sprawdzam status OpenSSH servera poprzez

```shell
$ sudo systemctl status ssh
```

![img9](./s9.png)

Sprawdzam ip do po��czenia si� przez ssh

![img10](./s10.png)

��cz� si� przez program `PuTTY` z maszyn� wirtualn� i si� loguj�

![img11](./s11.png)

![img12](./s12.png)

Nast�pnie przechodz� do instalacji dockera. W tym celu aktualizuje listy paczek z repozytori�w

```shell
sudo apt-get update
```

![img13](./s13.png)

Doinstalowa�em szereg wymaganych dependencji

```shell
$ sudo apt-get install \
>     ca-certificates \
>     curl \
>     gnupg \
>     lsb-release
>     
```

![img14](./s14.png)

Doda�em oficjalne klucze GPG dockera

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Ustawi�em repozytorium na `stable`

```shell
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Na koniec zainstalowa�em **Docker Engine**

```shell
 $ sudo apt-get update
 $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

![img15](./s15.png)

![img16](./s16.png)

---

## **Podpunkt 4**

Uruchamiam �rodowisko dockera

```shell
$ sudo service docker start
```

Sprawdzam dzia�anie

![img17](./s17.png)

![img18](./s18.png)

Nast�pnie pobra�em i uruchomi�em obraz linuxa

![img19](./s19.png)

Sprawdzono pobran� wersj� obrazu Ubuntu

![img20](./s20.png)

![img21](./s21.png)

---

## **Podpunkt 5**

Za�o�y�em konto w serwisie **Docker Hub**

![img22](./s22.png)

![img23](./s23.png)