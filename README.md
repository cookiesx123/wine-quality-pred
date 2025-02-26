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

# In English:
# **Wine Quality Prediction (Rating 1-10) Using Linear Regression in Python**  
### **Authors:**  
- Jagoda Radomska  
- Szymon Urbala - [@urbull](https://github.com/urbull)  

## **About the Project:**  
Modeling the prediction of red wine quality on a scale from 1 to 10. We used linear regression and conducted statistical tests to verify whether all assumptions were met.  

## **Data Source:**  
[UCI Machine Learning Repository - Wine Quality Dataset](https://archive.ics.uci.edu/dataset/186/wine+quality)  
We used red wine data.  

## **Variable Description:**  
### **Dependent Variable:**  
| Name   | Description | Unit |  
|--------|------------|------|  
| quality | Wine quality (rating based on consumer perception) | Rating 1-10 |  

### **Potential Independent Variables:**  
| Name | Description | Unit |  
|------|------------|------|  
| fixed_acidity | Fixed acidity; most acids present in wine | g/L |  
| volatile_acidity | Volatile acidity; acetic acid in wine (if excessive, it creates an unpleasant vinegar taste) | g/L |  
| citric_acid | Citric acid; in small amounts, it adds "freshness" | g/L |  
| residual_sugar | Residual sugar; the amount of sugar remaining after fermentation (rarely below 1g/L in wines) | g/L |  
| chlorides | Chlorides; amount of salt in wine | mg/L |  
| free_sulfur_dioxide | Free sulfur dioxide; a byproduct of fermentation | mg/L |  
| total_sulfur_dioxide | Total sulfur dioxide; wines without added sulfur dioxide taste more authentic | mg/L |  
| density | Density; should be close to the density of water | g/cm³ |  
| pH | pH level; red wine should have a pH between 3 and 4 | Scale 1-14 |  
| sulphates | Sulfates; wines without added sulfates taste more authentic | mg/L |  
| alcohol | Alcohol content | % |  

## **Project Structure:**  
| File | Description |  
|------|------------|  
| 📄 wine_quality_pred.ipynb | Notebook analyzing the full dataset |  
| 📄 wine_quality_pred_final.ipynb | Notebook analyzing a representative sample - final model |  
| 📊 winequality-red.xlsx | Full dataset in .xlsx format |  
| 📊 winequality-red-final.xlsx | Representative sample in .xlsx format |  

## **Project Stages:**  
### The following steps are included in the notebooks *wine_quality_pred.ipynb* and *wine_quality_pred_final.ipynb*:  
- Variable selection (Quasi-constant test, correlation matrix analysis)  
- Detection of outliers (identification of outliers, leverage points, and removal of influential observations - our dataset is not a representative sample, so we could afford to remove them)  
- Re-selection of variables after removing influential observations (correlation matrix analysis)  
- Multicollinearity analysis (Variance Inflation Factor - VIF)  
- Residual randomness analysis (Runs test)  
- Residual normality test (Shapiro-Wilk test)  
- Autocorrelation analysis (Durbin-Watson test, Breusch-Godfrey test)  
- Homoscedasticity test (White's test, calculated "for fun" since our data was not a time series 🙂)  

## **Problems and Solutions:**  
The notebook *wine_quality_pred.ipynb* includes additional attempts to improve the model. While working with the full dataset, we encountered issues that prevented successful modeling: residuals were not random, they did not follow a normal distribution, and autocorrelation was present.  

We examined the distributions of observations and residuals, attempted to transform variables with logarithmic-like distributions into their logarithms, obtained more observations, and even experimented with AI-generated data.  

The solution was to reduce the number of observations and create a representative sample. Further analysis on this sample was conducted in *wine_quality_pred_final.ipynb*, where our model met all linear regression assumptions, leading to successful modeling.  

## **Model Fit:**  
- The model from *wine_quality_pred.ipynb* had an R² coefficient of **0.38** – meaning that **38% of the total variability** in wine quality ratings was explained by the model, while **62% remained unexplained** due to factors not included in the model.  
- The model from *wine_quality_pred_final.ipynb* had an R² coefficient of **0.50** – meaning that **50% of the total variability** in wine quality ratings was explained by the model, while **50% remained unexplained** due to other factors.  

Although the second model had a better fit, an R² of **0.50** is still relatively low.  

## **Conclusions:**  
A different model, such as **logistic regression**, might be better suited for predicting red wine quality.  

