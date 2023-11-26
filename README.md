<h1>Laboratorium 5 - sprawozdanie obowiazkowe</h1>
<h2>Dominika Skolimowska, I2S2.4</h2>
<br />
<p>
  Utworzenie przestrzeni nazw odbylo sie z wykorzystaniem polecenia:
  <i>kubectl create namespace zad5</i> 
</p>
<p>
  1. Plik manifestu, definiujacy ograniczenia (quota) dla przedstrzeni nazw <i>zad5</i> nosi nazwe <i>zad5_quota.yaml</i>. Plik ten zostal uruchomiony poleceniem: <i>kubectl apply -f zad5_quota.yaml. </i>Poprawnosc wykonania tego zadania zostala potwierdzona poleceniem: <i>kubectl describe quota -n zad5</i>, ktorego wynik jest nastepujacy:
<br />
  <image src="quota.png" />
</p> 
<p>
  2. Plik manifestu, ktory tworzy poda <i>worker</i> w przestrzeni <i>lab5</i>, nazywa sie <i>zad5_worker.yaml</i>. Ponownie uruchomiono plik z wykorzystaniem polecenia <i>kubectl apply</i>. Poprawnosc wykonania zadania zostala sprawdzona poleceniem: <i>kubectl get pod -n zad5</i>. Uzyskano nastepujacy wynik:
  <br />
  <image src="worker.png" />
</p>
<p>
  3. W tym zadaniu zmodyfikowany zostal przyklad z poprzednich laboratoriow. Zmodyfikowany plik manifestu nosi nazwe <i>zad5_dep_ser.yaml</i>. Ponownie zostal on uruchomiony tym samym poleceniem. Wykonanie zadania zostalo sprawdzone poleceniem: <i>kubectl get deployment,service -n zad5</i>. Oto jego wynik:
  <br />
  <image src="depser.png" />
</p>
<p>
 4. Plik manifestu definiujacy HorizontalPodAutoscaler nosi nazwe <i>zad5_hpa.yaml</i>. Wartosc maxReplicas jest rowna 7. Przy zalozeniu, ze pojedynczy pod zuzywa maksymalne zasoby (250m CPU, 250 Mi RAM) zdefiniowane w pliku <i>zad5_dep_ser.yaml</i>, obliczona zostala maksymalna liczba podow, ktore moga jednoczesnie dzialac w ramach okreslonych limitow (CPU: 2000m, CPU na poda: 250m). Nalezy jednak pamietac, ze w przestrzeni nazw <i>zad5</i> jest juz pod <i>worker</i>, ktory przy maksymalnym zuzyciu zasobow zabiera 200m CPU.
  <br />
  Obliczenie: <i>(2000m-200m)/250m = 7.2</i>
  <br /> Jednak nalezy pamietac, ze liczba podow zostala ograniczona w quota do 10. Nalezalo wybrac mniejsza liczbe, czyli 7.
  <br /> Wynik dzialania wprowadzonych zmian zostal sprawdzony poleceniem <i>kubectl get hpa -n zad5</i>:
  <br />
  <image src="hpa.png" />
</p>
<p>
  5. Obiekty deklarowane w plikach yaml byly tworzone w kazdym podpunkcie.
</p>
<p>
  6. Niestety, w tym wypadku pojawil sie problem z poleceniem generujacym obciazenie, ktore bylo sugerowane w poprzednim laboratorium oraz w dokumentacji. Zamiast niego wykorzystano polecenie w postaci: <i>ab -c 10 -n 1000 http://adres-ip-uslugi/php-apache-service</i>. Rownoczesnie odbywalo sie monitorowanie wynikow polecenia <i>kubectl get hpa -n zad5 --watch</i>. Liczba replik zazwyczaj oscylowala w okolicy 5, ale zdarzaly sie sytuacje, w ktorych osiagala 7.
</p>
