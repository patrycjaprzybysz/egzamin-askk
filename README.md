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











1.1 Utwórz plik z obrazem Dockerfile, w którym z hosta do kontenera kopiowany będzie folder code (zawiera np. jeden skrypt w języku Python 🐍) i zbuduj go:
uruchom ww. skrypt wewnątrz kontenera.


1. zbudowanie obrazu dockera
```
docker build -t python-script .
```
2. uruchomienie kontenera z obrazem
```
docker run --rm python-script
```

2.1. Skopiuj wybrany plik tekstowy z hosta (swojego komputera) do kontenera Dockerowego.

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

3.1. Skopiuj wybrany plik tekstowy z kontenera Dockerowego do hosta (swojego komputera).

1. 

