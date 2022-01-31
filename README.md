# Wykrywanie dronów na obrazach z kamer CCTV przy użyciu algorytmu YOLOv5
<p align="center">
<img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/drone%20IR.jpg"/>
</p>

[link do projektu w Google Collab](https://colab.research.google.com/drive/10l6bnEOgIV99nO5su4MJWXQotTJ9-Mf1?usp=sharing)

## Cel i zarys problemu
Firma <b>NODRONE Co.</b> współpracująca z miastem Stołecznym Warszawa projektuje system wykrywania dronów w obrębie stref z zakazem lotów dronami tzw. No Drone Zone. Firma powierzyła mi opracowanie detekcji dronów na podstawie zdjęć z kamer CCTV w obrębie wydzielonych stref No Drone Zone. Celem jest detekcja dronów za pomocą odpowiednio dobranego algorytmu wykrywania obrazów, co pozwoli na rozwinięcie systemu powiadamiania służb o ewentualnych nieautoryzowanych przelotach.
## Algorytm YOLOv5
W mojej pracy wykorzystuję algorytm sieci neuronowej YOLOv5 do analizy obrazów. Algorytm jest udostępniony dzięki serwisowi [Roboflow]( https://roboflow.com/). YOLO (<b>Y </b> OU <b>O </b> NLY <b>L </b> OOK <b>O </b> NCE) należący do głębokich sieci konwolucyjnych (CNN) stosuje się do wykrywania obiektów na obrazach o dużej rozdzielczości.
W praktyce, algorytm YOLO nie tylko klasyfikuje obiekt lub obiekty widoczne na zdjęciu, ale również lokalizację konkretnego obiektu w postaci ramki. 
Algorytm ten potrafi przetwarzać obraz na macierz za pomocą operacji konwolucji, a trenując model  YOLO do wykrywania danego obiektu, de facto dostosowując wagi jądra konwolucyjnego, umożliwia detekcję nawet niewielkich obiektów na zdjęciu.  
YOLO dzieli obraz na system siatek lub regionów, a w każdej siatce stara się przewidzieć kilka parametrów dla wykrywanego obrazu m.in.: wielkość i położenie. W następnym kroku nakłada na obiekt ramkę tzw. bounding box, a potem usuwa szumy, biorąc po uwagę zmienną szacującą (score). Im większa wartość zmiennej szacującej, tym większe prawdopodobieństwo znalezienia danego obiektu, a więc większe prawdopodobieństwo, że utworzony bounding box nie zostanie usunięty i faktycznie otacza wykrywany obiekt. Algorytm YOLO wymaga niewielu zasobów obliczeniowych, przy zachowaniu dość dobrej skuteczności dopasowania.

# Etapy pracy
Aby wytrenować model detekcji dronów potrzebne są następujące etapy:
* Wgranie oznaczenie i wstępna obrazów ze zbioru treningowego na stronie mojego projektu w serwisie Roboflow
* Instalacja i pobranie potrzebnych bibliotek potrzebnych do detekcji obiektów algorytmem YOLOv5
* Konfiguracja zbioru treningowego YOLOv5
* Trenowanie YOLOv5
* Ocena wydajności i przydatności YOLOv5
* Wizualizacja danych treningowych YOLOv5
* Testowanie YOLOv5 na przykładowych obrazach
* Wnioski

## Wgranie oznaczenie i wstępna obróbka obrazów
Serwis Roboflow umożliwia wgrywanie analizowanego zbioru danych w postaci obrazów o różnych rozszerzeniach. Załadowałem 200 zdjęć dronów, które podzieliłem na zbiór testowy treningowy i walidacyjny w następujący sposób:

<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/zbiory.jpg"/>
</p>
 
Pozdzielenie zbioru w stosunku treningowego : walidacyjnego : testowego w stosunku 7:2:1 pozwala na optymalne uczenie algorytmu.</br>
Po załadowaniu obrazy zostały oznaczone na stronie mojego projektu przez polecenie „Annotate”, co umożliwia potem utworzenie zbioru treningowego oznaczonych obiektów.</br>
Wstępne przetwarzanie obrazu umożliwiło:
* Pozbycie się znaczników (jeśli takowe były) oraz autoorientację obrazów
* Dostosowanie rozmiaru obrazu do sieci neuronowej, do szybszego i skuteczniejszego uczenia sieci.
  
<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/Procesowanie%20wstepne.jpg" />
</p>
Po tym kroku wstępnie przygotowałem środowisko pracy klonując repozytowium YOLOv5 ze strony [Ultralytics](https://github.com/ultralytics/yolov5), a następnie instalując potrzebne biblioteki w tym bibliotekę pyTorch.
Załadowałem także moduły pozwalające na wyświetlanie obrazów, a także pobieranie modeli oraz danych


## Pobieranie danych z serwisu Roboflow
W ostatnim kroku przygotowane dane zostały udostępnione w formie linka. Zbiór danych z Roboflow eksportuję w formacie "YOLOv5 PyTorch".

 

 
________________________________________
<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/link.jpg" />
</p>
</br>
<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/wybor.jpg" />
</p>

Wklejam wygenerowany link z moim projektem z serwisu Roboflow (plik .zip) i rozpakowuję go

## Opisanie konfiguracji modelu i jego architektury
Aby model działał należy napisać skrypt w formacie YAML, który opisuje parametry modelu: warstw, klas itp. Korzystam z rekomendowanych ustawień serwisu Roboflow.
<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/params.jpg" />
</p>
</br>
## Trenowanie modelu detekcji dronów za pomocą algorytmu YOLOv5

Wytrenowałem model YOLOv5 dla 200 epok
<p align="center">
  <img src="https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/train.jpg" />
</p>
</br>

________________________________________
## Ocena wydajności detekcji dronów algorytmem YOLOv5

Wydajność trenowania modelu można zapisać w Tensorboardzie oraz w pliku results.txt
<p align="center">
  <img src=" https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/tensorboard.JPG" />
</p>

Następnie sprawdziłem stworzone wykresy oceny wydajności oceny wydajności parametrów takich jak m.in. precyzja, dokładność 
<p align="center">
  <img src=" https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/wykresy.PNG" />
</p>
## Wizualizacja danych treningowych ze znacznikami

Zapisałem ramkę z przykładowymi zdjęcia z oznaczeniem dronów w tzw. boxach 
<p align="center">
  <img src=" https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/drony_boxy.JPG" />
</p>

Można również spojrzeć na oznaczenie wszystkich obrazów ze zbioru testowego

<p align="center">
  <img src=" https://github.com/TheLordWeirdSloughFeg/proj_wykr_dron/blob/main/obrazki/drony_boxy_test.JPG" />
</p>

# Wnioski
Algorytm YOLO w wersji 5 dobrze wykrywa drony i nadaje się do zastosowania w systemie wczesnego ostrzegania. Precyzja przy 200 epokach przekracza 0.8, a parametr recall jest dostaczenie dobry (ok. 0,65). Algorytm YOLOv5 nadaje się także do wykrywania obiektów na filmie, co można by było wykorzystać bezpośrednio w oprogramowaniu kamer na miejscu obserwacji, jednak serwis Roboflow nie udostępnia tej opcji za darmo. W dalszym kroku mojej współpracy z Firmą NODRONE Co. powinienem zaprojektować aplikację, dzięki której wykrycie drona na danej klatce obrazu z kamery CCTV, po zastosowaniu mojego modelu, może generować alert w systemie wczesnego ostrzegania lub generować wiadomości SMS do grupy pilnującej strefy bez dronów.

