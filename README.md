# egzamin-askk


1. Utwórz plik z obrazem Dockerfile, w którym z hosta do kontenera kopiowany będzie folder code (zawiera np. jeden skrypt w języku Python 🐍) i zbuduj go:
uruchom ww. skrypt wewnątrz kontenera.
2. Skopiuj wybrany plik tekstowy z hosta (swojego komputera) do kontenera Dockerowego.
3. Skopiuj wybrany plik tekstowy z kontenera Dockerowego do hosta (swojego komputera).
4. Pokaż działanie komend ENTRYPOINT i CMD w wybranym projekcie.
5. Pokaż działanie usługi bazodanowej z wykorzystaniem docker-compose.
6. Pokaż działanie komend ADD i COPY i WORKDIR w wybranym projekcie.
7. Pokaż działanie docker compose w swoim projekcie.
8. Omów na podstawie swojej aplikacji komendy docker inspect i docker logs.
9. Czym są sieci w Dockerze? Zaprezentuj przykład na bazie swojego projektu.
10. Jaka jest różnica między obrazem i kontenerem? Pokaż przykład budowania obrazu (Dockerfile) i uruchamiania na jego podstawie kontenera.
11. Pokaż jak "wejść" do wybranego kontenera.
  Utwórz w nim plik tekstowy z dowolnymi danymi. Co zrobić, żeby po zamknięciu kontenera dane z pliku były dostępne po ponownym uruchomieniu kontenera?
  Zademonstruj dowolny sposób.
12. Zbuduj wybrany przez siebie obraz, nadaj mu 'tag' i opublikuj na DockerHubie. Następnie usuń lokalnie ww. obraz i pobierz go z DockerHuba.

****







****

**1.1 Utwórz plik z obrazem Dockerfile, w którym z hosta do kontenera kopiowany będzie folder code (zawiera np. jeden skrypt w języku Python 🐍) i zbuduj go:
uruchom ww. skrypt wewnątrz kontenera.**


1. zbudowanie obrazu dockera
```
docker build -t python-script .
```
2. uruchomienie kontenera z obrazem
```
docker run --rm python-script
```


**2.1. Skopiuj wybrany plik tekstowy z hosta (swojego komputera) do kontenera Dockerowego.**


1. stworzenie kontenera
```
docker run -dit --name mycontainer python:3.9-slim
```
2. stworzenie katalogu
```
docker exec mycontainer mkdir -p /app
```
3. skopiowanie pliku do kontenera
```
docker cp myfile.txt mycontainer:/app/myfile.txt
```
4. wejście do kontenera
```
docker exec -it mycontainer bash
```
5. wejscie do katalogu
```
cd /app
```
6. wyswietlenie zwartosci kontenera (plik myfile.txt)
```
cat myfile.txt
```


**3.1. Skopiuj wybrany plik tekstowy z kontenera Dockerowego do hosta (swojego komputera).**


1. sprawdzenie zawartosci kontenera
```
docker exec mycontainer find /
```

2. kopiowanie pliku txt z kontenera do hosta
```
docker cp mycontainer:/app/container_file.txt ./container_file.txt
```


**4.1 Pokaż działanie komend ENTRYPOINT i CMD w wybranym projekcie**


1. zbudowałam dockerfile z cmd

```
docker build -f cmd.Dockerfile -t cmd .
```
2. uruchamiam kontener z nowym poleceniem (reszta polecen sie nadpisuje i zostanie wykonane tylko to osttanie)

```
docker run cmd ls
```
![image](https://github.com/user-attachments/assets/a32dacb6-803b-4f68-afef-cb9f1b5b2388)

3. zbudowałam dockerfile z entrypoint

```
docker build -f entrypoint.Dockerfile -t entrypoint .
```

4. uruchamiam kontener z nowym poleceniem (zostanie dodane na koncu to polecenie jako argument dopiero gdy dodam flage --entrypoint to zostanie nadpisane)

```
docker run entrypoint ls
```
```
docker run --entrypoint ls entrypoint
```

**5.1 Pokaż działanie usługi bazodanowej z wykorzystaniem docker-compose.**


1. uruchomienie docker-compose

```
docker-compose up -d
```

2. zalogowanie sie do kontenera
```
docker exec -it my_postgres bash
```
3. połaczenie z baza danych
```
psql -U exampleuser -d exampledb
```
4. dodanie danych do tabeli
```
INSERT INTO users (name, email)
VALUES ('John D', 'john.d@example.com');
```
5. sprawdzenie danych
```
SELECT * FROM users;
```


**6.1 Pokaż działanie komend ADD i COPY i WORKDIR w wybranym projekcie.**


1. 


**7.1 Pokaż działanie docker compose w swoim projekcie.**
docker-5


**8.1 Omów na podstawie swojej aplikacji komendy docker inspect i docker logs.**

```docker ps```

```docker inspect``` zawiera wszytskie informacje o kontenerze, jak nazywa się jego sieć z jakiego portu korzysta, jaki ma obraz, czego uzywa dockerfile (cmd). ```docker logs``` służy do wyświetlania dzienników kontenera. Pozwala na przeglądanie wszystkich logów wypisywanych przez procesy wewnątrz kontenera.

```docker inspect:``` Używane do uzyskania szczegółowych informacji o kontenerze, obrazie, sieci, woluminach itd. Wynik jest w formacie JSON, ale można go filtrować, aby uzyskać tylko określone dane (np. adres IP kontenera).
```docker logs:``` Używane do przeglądania logów kontenera. Może być pomocne do debugowania i monitorowania kontenerów, zwłaszcza podczas analizy problemów z uruchomionymi aplikacjami w kontenerach.


**9.1 Czym są sieci w Dockerze? Zaprezentuj przykład na bazie swojego projektu.**

W Dockerze sieci (ang. networks) służą do umożliwienia komunikacji między kontenerami. Każdy kontener jest domyślnie częścią jednej sieci (np. sieci bridge), ale można tworzyć niestandardowe sieci, aby kontenery mogły się ze sobą komunikować w bardziej kontrolowany sposób. Sieci w Dockerze pomagają zarządzać ruchem między kontenerami oraz ustawić, które kontenery mogą się ze sobą łączyć.

Docker oferuje kilka typów sieci:

* Bridge – Sieć typu mostu, domyślna dla kontenerów. Kontenery w tej samej sieci mogą się ze sobą komunikować, ale nie mają dostępu do zewnętrznego świata, jeśli nie zostanie to skonfigurowane.
* Host – Kontener używa sieci hosta, co oznacza, że kontener i host mają wspólną przestrzeń sieciową.
* None – Kontener nie jest połączony z żadną siecią.
* Custom – Sieci użytkownika, które można konfigurować na własne potrzeby.

```
docker-compose up --build
```


**10.1 Jaka jest różnica między obrazem i kontenerem? Pokaż przykład budowania obrazu (Dockerfile) i uruchamiania na jego podstawie kontenera.**

docker-9

Obraz (ang. image) to statyczny szablon, który zawiera wszystkie niezbędne pliki, zależności i konfigurację do uruchomienia aplikacji w kontenerze. Obrazy są niezmienne i przechowywane w rejestrach, takich jak Docker Hub. Można je porównać do szablonów maszyn wirtualnych lub obrazów systemu operacyjnego.

Kontener (ang. container) to instancja uruchomionego obrazu. Kontener działa na bazie obrazu i jest dynamiczny – może być uruchamiany, zatrzymywany, modyfikowany i usuwany. Kontenery są izolowane od siebie i od systemu operacyjnego hosta. Kontener jest procesem działającym w środowisku wirtualnym i zawiera wszystko, co jest potrzebne do uruchomienia aplikacji.

1. Obraz to statyczny plik, który jest używany do tworzenia kontenerów.
2. Kontener to działający proces, który powstał na podstawie obrazu.
3. Obrazy są trwałe i niezmienne, kontenery mogą być tymczasowe, dynamiczne i zmieniają się w czasie działania.

![image](https://github.com/user-attachments/assets/673c3a6c-6807-4ff0-8366-9bfdc5ffc9c9)

* **FROM python:3.8-slim:** Używamy oficjalnego obrazu python:3.8-slim jako bazy. Jest to lekka wersja obrazu Python 3.8.
* **WORKDIR /usr/src/app:** Ustawiamy katalog roboczy, w którym będziemy pracować w kontenerze.
* **COPY requirements.txt ./:** Kopiujemy plik requirements.txt z lokalnego systemu do kontenera.
* **RUN pip install --no-cache-dir -r requirements.txt:** Instalujemy zależności Pythona, jeśli są one określone w requirements.txt.
* **COPY app.py ./:** Kopiujemy aplikację app.py do kontenera.
* **CMD ["python", "app.py"]:** Określamy, że po uruchomieniu kontenera ma zostać uruchomiona aplikacja Python (app.py).

* budowanie obrazu z dockerfile ```docker build -t my-python-app . ```
*uruchamianie kontenera ```docker run --name my-python-container my-python-app ```


**11.1 Pokaż jak "wejść" do wybranego kontenera.
Utwórz w nim plik tekstowy z dowolnymi danymi. Co zrobić, żeby po zamknięciu kontenera dane z pliku były dostępne po ponownym uruchomieniu kontenera?
Zademonstruj dowolny sposób.**



**12.1 Zbuduj wybrany przez siebie obraz, nadaj mu 'tag' i opublikuj na DockerHubie. Następnie usuń lokalnie ww. obraz i pobierz go z DockerHuba.**


