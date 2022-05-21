
# Projekt 
## Rosiak B�a�ej
### Przygotowujemy pipeline
Niniejsze sprawozdanie zawiera przebieg realizacji projektu dotycz�cego przygotowania _pipeline_. Ze wzgl�du na charakter zadania oraz wymaganie, �eby wi�kszo�� os�b by�a w stanie odtworzy� etapy budowania artefaktu, j�zyk techniczny/fachowy b�dzie ograniczony, natomiast b�dzie mo�na w wielu miejscach zauwa�y� �argon, por�wnania oraz uproszczenia.

Po co wi�c budowa� pipeline? Jest to zwi�zane z pewnymi powtarzalnymi etapami, kt�re praktycznie zawsze trzeba wykona� w celu dostarczenia �dzia�aj�cego� produktu (dzia�aj�cego bo wst�pnie spe�nia swoje zadanie, ale zawsze znajd� si� jakie� bugi). Pipeline budujemy po to, by zautomatyzowa� te czynno�ci � czyli by u�atwi� sobie prac�. Zazwyczaj taki pipeline  obejmuje automatyzacj� budowania projektu, jego testowanie, walidacj� i raportowanie. W pipeline mog� wyst�powa� pewne zdarzenia, kt�re mog� wymaga� interwencji cz�owieka.

W skr�cie � projekt polega� na tym, by przygotowa� odpowiednie pliki _DOCKERFILE_ oraz _PIPELINE_, kt�re nale�a�o wrzuci� na repozytorium. _Jenkins_, kt�ry zosta� ju� zainstalowany i skonfigurowany w ramach poprzedzaj�cych zaj��. Tam tworzony jest projekt, kt�ry na samym pocz�tku pobiera potrzebne pliki z repozytorium z odpowiedniej ga��zi, a nast�pnie wykonuje kolejno etapy wed�ug przepisu podanego w _jenkinsfile_. Je�eli wszystkie etapy zako�cz� si� powodzeniem oraz zaznaczyli�my opcje, �e chcemy promowa� projekt to zostanie zbudowany artefakt _calculator_X.jar_, gdzie _X_ jest wersj�, kt�r� podali�my.

Na pocz�tku nale�a�o by uruchomi� naszego _Jenkinsa_, kt�rego na tym etapie powinni�my mie� skonfigurowanego. Nale�y uruchomi� kontener _DIND_ (bo inaczej w _pipeline�ie_ nie b�d� dzia�a�y praktycznie �adnego instrukcje _docker_) oraz samego _Jenkinsa_. Odpalono je z pomoc� dokumentacji _Jenkinsa_ ze strony [https://www.jenkins.io/doc/book/installing/docker/](https://www.jenkins.io/doc/book/installing/docker/).  
Uruchomienie _dind�a_:
> docker run \
  --name jenkins-docker \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2

Uruchomienie _jenkins�a_:

> docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.332.3-1 

![](1.png)
![](2.png)
_Zdaj� sobie spraw�, �e komenda sudo mo�e frustrowa�, lecz wyszed�em z za�o�enia, �e s� to tylko zaj�cia laboratoryjne, kt�re maj� tylko nauczy� pos�ugiwa� si� Jenkinsem i pipelinami. Podejrzewam, �e w normalnym przypadku konto dla pracownika DevOps by�o by tak skonfigurowane, by nie musia� u�ywa� polecenia sudo � jest wi�c to co� co raczej powinno nale�e� do administratora system�w._

Kiedy _Jenkins_ si� uruchomi�, mo�na si� zabra� za przygotowanie plik�w do _pipeline_. ��cznie stworzono 4 pliki � 3 pliki _dockerfile_ dla etap�w _build_, _test_ oraz _deploy_.

Dockerfile _builder_ odpowiada za �ci�gni�cie projektu z repozytorium na wolumin wej�ciowy _input_v_ (**git clone**) a nast�pnie zbudowanie projektu (**mvn package**) i przekopiowanie go na wolumin wyj�ciowy _output_v_ (**cp -r target /output_v/**). Dockerfile buduje obraz na bazie obrazu _maven_.
![](3.png)
Dockerfile _tester_ odpowiada za przetestowanie projektu (**mvn test**), kt�ry znajduje si� na woluminie wej�ciowym. Ten dockerfile buduje obraz na bazie obrazu _builder_.
![](4.png)
Dockerfile _deploy_ odpowiada za sprawdzenie czy zbudowany plik _jar_ dzia�a w �rodowisku konsumenckim. Tak wi�c nie mo�na budowa� obrazu na bazie _buildera_, lecz na bazie innego � w tym przypadki _maven�a_. W celu u�atwienia zadania _Dockerfile_ zbudowano w taki spos�b, by w�a�ciwie uruchamia� program i ko�czy� dzia�anie programu poprzez wpisanie 5 (_program konsolowy_).
![](5.png)
Mo�na powiedzie�, �e pipeline jest podzielony na 4 g��wne etapy � Build, Test, Deploy i Publish. Kroki Build, Test i Deploy zosta�y podzielone na 2 podetapy � pierwszy z nich przygotowuje odpowiedniego agenta bazuj�cego na odpowiednim _Dockerfile_. Dodatkowo pojawia si� krok Prepare do przygotowania �rodowiska do stworzenia artefaktu. Pipeline dodatkowo przyjmuje 2 parametry:

 - PROMOTE � typu boolean - informuje o tym czy ma by� budowany i publikowany artefakt � sprawdzane jest to przed etapem publish � domy�lnie na _false_.

- VERSION � typu string � zawiera informacje odno�nie wersji artefaktu, kt�ry jest dopisywany na koniec nazwy pliku _jar_ (je�eli opcja _PROMOTE_ jest zaznaczona) � domy�lnie na 1.0.0

Jest te� na samym ko�cu _post_ � _always_ � blok instrukcji, kt�ry zawsze powinien si� wykona�. Wykorzystywany jest jako swego rodzaju czy�cioch.

> pipeline {
    agent any
    parameters {
        string(name: 'VERSION', defaultValue: '1.0.0', description: '')
        booleanParam(name: 'PROMOTE', defaultValue: false, description: '')
    }
    stages {
    	stage('Prepare') {
    	    steps {
            	sh 'echo Uruchomiono Prepare'
    	    	sh 'mkdir publish -p'
    	    	sh 'ls publish'
    	    	sh 'pwd'
    	        sh 'chmod 777 -R publish'
		sh 'docker volume prune -f'
    	    	sh 'docker volume create --name input_v'
    	    	sh 'docker volume create --name output_v'
    	    }
    	}
        stage('Build 1') {
            steps {
                sh 'echo Uruchomiono Build 1'
                sh 'docker build -t lab05_builder . -f ITE/GCL04/BR404123/Lab05/dockerfile_builder'
                sh 'ls'
            }
        }
	stage('Build 2'){
	    agent {
		docker {
		    image'lab05_builder'
                    args '-v input_v:/input_v -v output_v:/output_v --user root'
                    reuseNode false
		}
	    }
	    steps {
		sh 'echo Uruchomiono Build 2'
		sh 'cp -r /input_v/target/* /output_v/'
		sh 'ls /output_v/'
	    }
	}
        stage('Test 1') {
            steps {
                sh 'echo Uruchomiono Test 1'
                sh 'docker build -t lab05_tester . -f ITE/GCL04/BR404123/Lab05/dockerfile_tester'
                sh 'ls'
            }
        }
	stage('Test 2') {
	    agent {
		docker {
		    image'lab05_tester'
                    args '-v input_v:/input_v --user root'
                    reuseNode false
		}
	    }
	    steps {
		sh 'echo Uruchomiono Test 2'
	    }
	}
        stage('Deploy 1') {
            steps {
                sh 'echo Uruchomiono Deploy'
                sh 'docker build -t lab05_deploy . -f ITE/GCL04/BR404123/Lab05/dockerfile_deploy'
                sh 'ls'
            }
        }
	stage('Deploy 2') {
	    agent {
		docker {
		    image'lab05_deploy'
                    args '-v output_v:/output_v --user root'
                    reuseNode false
		}
	    }
	    steps {
		sh 'echo Uruchomiono Deploy 2'
	    }
	}
        stage('Publish') {
            when {
                environment name: 'PROMOTE', value: "true"
            }
	    agent {
		docker {
		    image'lab05_builder'
                    args '-v output_v:/output_v --user root'
                    reuseNode false
		}
	    }
            steps {
                sh 'echo Uruchomiono Publish'
                sh 'ls'
		sh 'echo ${VERSION}'
		sh 'cp -r /output_v/ ./publish/'
		sh 'ls publish'
		sh 'mv publish/calculatorDevOps-1.0-SNAPSHOT-jar-with-dependencies.jar	 publish/calculator_${VERSION}.jar'
		sh 'ls publish'
		sh 'pwd'
                archiveArtifacts artifacts: 'publish/calculator_*.jar', fingerprint: true
		sh 'rm -rf publish'
            }
        }
    }
    post {
    	always {
	    sh 'echo Czyszchoch'
            sh 'ls publish'
	    sh 'pwd'
    	    sh 'chmod 777 -R publish'
    	    sh 'rm -rf publish'
    	}
   }
}

Maj�c tak przygotowane pliki wrzucone na GIT�a mo�na zabra� si� za samego Jenkins�a. Wiedz�c po ostatnich zaj�ciach jaki adres IP ma VM oraz na jakim porcie odpalono Jenkins�a mo�na wej�� do niego przez przegl�dark�. Po zalogowaniu tworzy si� Nowy Projekt wybieraj�c przy tym Pipeline i podaj�c nazw� projektu. W nast�pnym oknie nale�y zwr�ci� uwag� na sekcj� _Pipeline_. Skrypt musi by� pobierany z _SCM_, a w polu _SCM_ nale�y wybra� okno GIT. Kolejne okna odno�nie GITa uzupe�nia si� dosy� prosto � link do repozytorium, nazwa brancha a tak�e �cie�k� do katalogu, gdzie znajduje si� pipeline.
![](6.png)
![](7.png)
![](8.png)
![](9.png)
Tak wi�c jest ju� projekt zbudowany, wi�c mo�na uruchomi� pipeline�a klikaj�c w opcj� _Uruchom z parametrami_ oraz uzupe�niamy pola.
![](10.png)
![](11.png)
Ca�y pipeline, pocz�wszy od kroku _Prepare_ a� po _Publish_ przebieg� pomy�lnie i naszym oczom ukaza� si� kalkulator z wersj�, kt�r� wcze�niej podano � 1.5.0.
Diagram aktywno�ci:
![](12.png)