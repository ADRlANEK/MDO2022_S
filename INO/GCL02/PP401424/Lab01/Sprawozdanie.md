# Sprawozdanie 1
### 07.03.2022r.

System kontroli wersji Git oraz narz�dzie s�u��ce do obs�ugi kluczy SSH jest domy�lnie instalowane przy instalacji systemu linux Ubuntu server, dlatego nie by�o konieczno�ci instalowania ich manualnie.

![git-install](./git-install.png)

Klonuj� repozytorium za pomoc� protoko�u **HTTPS**.

![clone-HTTPS](./clone-HTTPS.png)

Generuj� nowy klucz **SSH**.

![ssh-key1](./ssh-key1.png)

Sprawdzam klucz publiczny oraz sprawdzam jego poprawno�� poprzez wygenerowanie go za pomoc� klucza prywatnego.

![ssh-key2](./ssh-key2.png)

Nast�pnie generuj� drugi klucz i sprawdzam go w ten sam spos�b. Obydwa klucze zosta�y zabezpieczone has�em.

![ssh-key3](./ssh-key3.png)

![ssh-key4](./ssh-key4.png)

Dodaje klucz publiczny do konta na **Github**.

![github1](./github1.png)

![github2](./github2.png)

Ponadto dodaje klucz prywatny do **`ssh-agent`**

![ssh-agent](./ssh-agent.png)

Narz�dzie **Git** mam ju� skonfigurowane.

![git-config](./git-config.png)

Klonuje repozytorium za pomoc� **SSH**. Operacja si� uda�a co �wiadczy o poprawnym wygenerowaniu i dodaniu kluczy.

![clone-ssh](./clone-ssh.png)

Prze��czam si� na ga��� **`main`**.

![main](./main.png)

Nast�pnie prze��czam si� na ga��� mojej grupy **`INO-GCL02`**.

![gcl02](./gcl02.png)

Tworz� ga��� **`PP401424`**, kt�ra wychodzi od ga��zi grupy, oraz tworz� odpowiedni katalog.

![mkdir](./mkdir.png)

Dodaje sprawozdanie oraz zatwierdzam zmiany za pomoc� `git add .`

![git-add](./git-add.png)

Tworz� commit z komentarzem.

![git-commit](./git-commit.png)

Wysy�am zmiany do zdalnego repozytorium.

![git-push](./git-push.png)