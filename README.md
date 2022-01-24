# proj_wykr_dron
Wykrywanie dronów na obrazach z kamer CCTV przy użyciu algorytmu YOLOv5
# Wstęp
Firma NODRONE Co. współpracująca z miastem Stołecznym Warszawa projektuje system wykrywania dronów w obrebie stref z zakazem lotów dronami tzw. No Drone Zone.
Firma powierzyła mi opracowanie detekcji dronów na podstawie zdjęć z kamer CCTV w obrębie wydzielonych stref No Drone Zone.
Celem jest detekcja dronów i powiadomienie służb o ewentualnych nieautoryzowanych przelotach.
### Algorytm YOLOv5
W mojej pracy wykorzystuję algorytm sieci neuronowej YOLOv5 do analizy obrazów. Algorytm jest udostępniony serwisowi [Roboflow](https://roboflow.com). 

### **Etapy pracy**
Aby wytrenować model detekcji dronów potrzebne sa następujące etapy:

*   Wgranie oznaczenie i wstępna obrazów ze zbioru treningowego na stronie mojego projektu w serwisie Roboflow
*   Instalacja i pobranie potrzebnych bibliotek potrzebnych do detekcji obiektów algorytmem YOLOv5
*   Konfigracja zbioru treningowego YOLOv5
*   Trenowanie YOLOv5
*   Ocena wydajnosci i przydatności YOLOv5
*   Wizualizacja danch treningowych YOLOv5
*   Testowanie YOLOv5 na przykładowych obrazach
*   Eksport wyników dla YOLOv5 dla przyszłych optymalizacji
