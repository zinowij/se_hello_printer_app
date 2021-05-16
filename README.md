# Simple Flask App

Aplikacja Dydaktyczna wyświetlająca imię i wiadomość w różnych formatach dla zajęć
o Continuous Integration, Continuous Delivery i Continuous Deployment.

- W projekcie wykorzystamy virtual environment, dla utworzenia hermetycznego środowisko dla aplikacji:

  ```
  # tworzymy hermetyczne środowisko dla bibliotek aplikacji:
  $ python3 -m venv .venv

  # aktywowanie hermetycznego środowiska
  $ source .venv/bin/activate
  $ pip install -r requirements.txt
  $ pip install -r test_requirements.txt

  # zobacz
  $ pip list
  ```

  Sprawdź: [tutorial venv](https://docs.python.org/3/tutorial/venv.html) oraz [biblioteki flask](http://flask.pocoo.org).

- Uruchamianie applikacji:

  ```
  # jako zwykły program
  $ python main.py

  # albo:
  $ PYTHONPATH=. FLASK_APP=hello_world flask run


  $ make deps
  $ make test
  $ make lint
  $ make file
  ```

- Uruchamianie testów (see: http://doc.pytest.org/en/latest/capture.html):

  ```
  $ PYTHONPATH=. py.test
  $ PYTHONPATH=. py.test --verbose -s
  ```

- Kontynuując pracę z projektem, aktywowanie hermetycznego środowiska dla aplikacji py:

  ```
  # deaktywacja
  $ deactivate
  ```

  ```
  ...

  # aktywacja
  $ source .venv/bin/activate
  ```

- Integracja z TravisCI:

  ```
  # miejsce na twoje notatki
  ```

# Pomocnicze

## Ubuntu

- Instalacja dockera: [dockerce howto](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## Centos

- Instalacja docker-a:

  ```
  $ yum remove docker \
        docker-common \
        container-selinux \
        docker-selinux \
        docker-engine

  $ yum install -y yum-utils

  $ yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo

  $ yum makecache fast
  $ yum install -y docker-ce
  $ systemctl start docker


      $ make docker_build
      $ make docker_run
      $ export DOCKER_PASSWORD=Te5ter123
      $ make docker_push
  ```


  https://app.statuscake.com/YourStatus2.php


  W tym ćwiczeniu przygotowujemy do produkcji naszą aplikację, w tym celu musimy przygotować monitoring. Budżet jest niski, terminy gonią, decydujemy się na prosty monitoring, który wykryje, kiedy jesteśmy offline - statuscake.com.
1. Przejdź do statuscake.com
2. Utwórz konto.
3. Dodaj grupę kontaktową ze swoim email-em.
4. Dodaj Uptime Monitoring test:
- URL: url Twojej aplikacji
- Nazwa: dowolna
- Contact Group: zdefiniowana w 3


https://app.statuscake.com/button/index.php?Track=TRACK_ID&Days=1&Design=1


Buttons:
Travis:
[![Build Status](https://travis-ci.org/zinowij/se_hello_printer_app.svg?branch=master&status=passed)](https://travis-ci.org/github/zinowij/se_hello_printer_app/builds/771226804)


statuscake:
![StatusCake](https://app.statuscake.com/button/index.php?Track=5961424&Days=1&Design=1)



Test Coverage

1. Dodaj pytest-cov, plugin do pytest, do analizy pokrycia testami kodu, do test_requirements.txt:
      $ echo 'pytest-cov' >> test_requirements.txt
      $ pip install -r test_requirements.txt
2. Teraz możemy wywołać py.test z aktywowanym pytest-cov (i wygenerować coverage.xml):
      $ PYTHONPATH=. py.test --verbose -s --cov=.
  Zamiast na ekran możemy przekierować raport do raportu XML:
      $ PYTHONPATH=. py.test --verbose -s --cov=. --cov-report xml
3. Dodajmy również tworzenie pliku junit:
$ PYTHONPATH=. py.test -s --cov=. --cov-report xml --junit-xml=test_results.xml
4. Dodaj dwa nowe targety do pliku Makefile:
- test_cov – wywłanie coverage z wypisaniem raportu na ekran
- test_xunit – generacja xunit i coverage
5. Dodaj do .gitignore, aby git (git status) ignorował pliki: test_results.xml, coverage.xml i .coverage. 6. Wykorzystaj make test_xunit w .travis.yml. Sprawdź, czy działa. Możliwe, że musisz przypiąć wersję
pytest w test_requirements.txt, np.:
pytest>=4.6
