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
  <image src=""></image>
</p> 
