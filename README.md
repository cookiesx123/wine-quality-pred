# Predykacja jakości wina (ocena 1-10) z użyciem regresji liniowej w języku Python
### Autorzy:
- Jagoda Radomska
- Szymon Urbala - [@urbull](https://github.com/urbull)
## O projekcie:
Modelowanie predykcji jakości czerwonego wina w skali od 1 do 10. Wykorzystaliśmy regresję liniową, wykonując testy statystyczne, by sprawdzić, czy wszystkie założenia zostały spełnione. 
## Źródło danych:
https://archive.ics.uci.edu/dataset/186/wine+quality
Użyliśmy danych o winie czerwonym.
## Opis zmiennych:
### Zmienna objaśniana:		
|nazwa |opis |jednostka|
|:-----|:----|:--------|
|quality |jakość wina (ocena na podstawie odczuć konsumentów)	|ocena 1-10|
		
### Potencjalne zmienne objaśniające:
|nazwa	|opis	|jednostka|
|:-----|:-----|:--------|
|fixed_acidicy	|kwasowość stała; większość kwasów zawartych w winie	|g/l|
|volatile_acidicy	|kwasowość lotna; kwas octowy zawarty w winie (jeśli jest go za dużo to wyczuwalny jest nieprzyjemny smak octu)	|g/l|
|citric_acid	|kwas cytrynowy; w małych ilościch dodaje "świeżości"	|g/l|
|residual_acid	|cukier resztkowy; ilość cukru pozostała po zakończeniu fermentacji (rzadko można znaleźć wino, które ma mniej niż 1g/l)	|g/l|
|chlorides	|chlorki; ilość soli w winie	|mg/l|
|free_sulfur_dioxide	|wolny dwutlenek siarki; produkt uboczny procesu fermentacji 	|mg/l|
|total_sulfur_dioxide	|całkowity dwutlenek siarki; wina bez dodatku dwutlenku siarczanu smakują autentyczniej	|mg/l|
|density	|gęstość; powinna być przybliżona do gęstości wody	|g/cm^3|
|pH	|pH; czerwone wino powinno mieć pH od 3 do 4	|1-14|
|sulphates	|siarczany; wina bez dodatku siarczanów smakują autentyczniej	|mg/l|
|alcohol	|alkohol; zawartość alkoholu	|%|

## Struktura projektu:
|Plik| Opis|
|:----------|:----|
|📄 wine_quality_pred.ipynb |Notebook z analizą pełnego zestawu obserwacji|
|📄 wine_quality_pred_final.ipynb |Notebook z analizą próbki reprezentatywnej obserwacji - końcowy model|
|📊 winequality-red.xlsx |Pełen zestaw obserwacji w pliku .xlsx|
|📊 winequality-red-final.xlsx |Próbka reprezentatywna obserwacji w pliku .xlsx|

## Etapy projektu:
### W notebookach wine_quality_pred.ipynb oraz wine_quality_pred_final.ipynb znajdują się następujące etapy:
- Dobór zmiennych (test Quasi-stałych, analiza macierzy korelacji)
- Wyszukanie obserwacji nietypowych (zidentyfikowanie obserwacji odstających, dźwigniowych oraz usunięcie obserwacji wpływowych - używana przez nas próbka danych nie jest próbką reprezentatywna, więc możemy sobie pozwolić na ich usunięcie)
- Ponowny dobór zmiennych po usunięciu obserwacji wpływowych (analiza macierzy korelacji)
- Badanie współliniowości (współczynnik współliniowości VIF)
- Badanie losowości reszt (test serii)
- Badanie normalności reszt (test Shapiro-Wilka)
- Badanie autokorelacji (test Durbina-Watsona, test Breuscha-Godfreya)
- Badanie homoskedastyczności (test White'a, policzony "dla sportu", gdyż nasze dane nie były szeregiem czasowym 🙂)
### Problemy i ich rozwiązania:
  W notebooku wine_quality_pred.ipynb znajdzują się dodatkowo próby naprawy modelu. Pracując na pełnym zestawie obserwacji, napotkaliśmy problemy, które uniemożliwiały zakończenie modelowania z sukcesem: okazało się, że reszty nie są losowe, nie mają rozkładu normalnego i wykazują autokorelację. Przyjrzeliśmy się dokładnie rozkładom obserwacji oraz reszt, spróbowaliśmy zamienić zmienne, które miały wykres zbliżony do logarytmicznego na ich logarytm, uzyskać więcej obserwacji czy nawet użyć obserwacji wygynerowanych przez AI. Rozwiązaniem problemu okazało się zmniejszenie liczby obserwacji i stworzenie próbki reprezentatywnej. Dalszą analizę na tej próbce przeprowadziliśmy w notebooku wine_quality_pred_final.ipynb - tam nasz model spełnił już wszystkie założenia regresji liniowej - modelowanie zakończyło się sukcesem.
### Dopasowanie modeli:
- model z pliku wine_quality_pred.ipynb miał współczynnik determinacji R^2=0,38 - 38% całkowitej zmienności oceny jakości wina zostało wyjaśnione modelem. Pozostałe 62,34% zmienności nie zostało wyjaśnione zawartymi w modelu zmiennymi objaśniającymi. Było to spowodowane działaniem innych czynników nieuwzględnionych w modelu.
- model z pliku wine_quality_pred_final.ipynb miał współczynnik determinacji R^2=0,5 - 50% całkowitej zmienności oceny jakości wina zostało wyjaśnione modelem. Pozostałe 50% zmienności nie zostało wyjaśnione zawartymi w modelu zmiennymi objaśniającymi. Było to spowodowane działaniem innych czynników nieuwzględnionych w modelu.

Drugi model był lepiej dopadsowany, jednak R^2=0,5 to dalej niezbyt wysoki wynik. 

### Wnioski:
Do wymodelowania problemu predykcji jakości wina czerwonego lepiej nadałby się inny model tj. regresja logistyczna.
