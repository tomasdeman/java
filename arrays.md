## Enkele voorbeelden van toepassingen op arrays

### Oefening 1: dobbelen

Schrijf een klasse Dobbelen waarbij volgende simulatie gebeurt: er wordt 100 keer gegooid, telkens \(per worp\) met 3 dobbelstenen.

In een array ogen wordt bijgehouden hoeveel maal het aantal ogen \(telkens de som van de drie dobbelstenen\) gegooid is.

Klasse `Dobbelen`:

Attributen:

* array ogen, die zal bijhouden hoeveel keer elk aantal ogen \(per worp, met 3 dobbelstenen\) gegooid wordt

Methoden:

* constructor: creëert de array

  * Andere methoden:

    * `dobbelsteenGooien()`:
      * declareert en genereert een randomgenerator
      * initialiseert de `array` ogen en simuleert het gooien
    * `toonResultaat()`: toont van elk aantal ogen hoeveel keer het gegooid werd.

      Het resultaat kan er als volgt uitzien:

    ![](/assets/nv2.png)

    Merk op dat je een normaalverdeling krijgt.

#### Uitbreidingsoefening:

In plaats van de output op de terminal te zetten met `System.out.println()`, zou je de normaalverdeling op een grafiek kunnen zetten met een _JavaFX_ `barChart`.  
Zoek online op hoe je deze kan gebruiken. Enkele voorbeelden van pagina's die je hierbij helpen:

* [https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm)
* [http://www.java2s.com/Tutorials/Java/JavaFX/0850\_\_JavaFX\_BarChart.htm](http://www.java2s.com/Tutorials/Java/JavaFX/0850__JavaFX_BarChart.htm)

### Oefening 2: Zeef van Eratosthenes

Dit is een algoritme waarmee je alle priemgetallen kan bepalen tot aan een zekere bovengrens.

Het algoritme werkt als volgt.

1. Creëer een array van booleans \(priem\). De bovengrens van deze array is het maximale getal dat je wil onderzoeken.  
   Als je dus wil weten welke priemgetallen er zijn met als maximumgrens 500, maak je een array met 501 elementen.

2. Zet alle elementen op `true`

3. Schrap als volgt alle niet-priemgetallen in de array door ze op `false` te zetten:

   1. Zet de eerste twee indexen van de array `priem` op false. We weten namelijk dat 0 en 1 geen priemgetallen zijn.

   2. Als je een priemgetal tegenkomt, moet je in de array `priem` alle veelvouden van dit priemgetal schrappen. Dit doe je door steeds een nieuwe lus te starten bij elk priemgetal je tegenkomt. Makkelijkst is dit binnen een andere methode te doen.

   3. Als je buitenste lus het maximum bereikt heeft, heb je alle priemgetallen gevonden.

4. Druk deze getallen af op de terminal \(10 per lijn\).

Wil je bijvoorbeeld de priemgetallen bepalen tot aan 1000, dan ga je als volgt te werk:

* Schrijf alle getallen van 2 tot 1000 op.
* Schrap alle veelvouden van 2.
* Het eerstvolgende getal dat nog niet geschrapt is, is 3. Schrap nu alle veelvouden van 3.
* Het eerstvolgende getal dat nog niet geschrapt is, is 5. Schrap nu alle veelvouden van 5.
* Door deze methode voldoende lang vol te houden vind je alle priemgetallen tussen 0 en 1000.

#### Uitdaging: houd bij hoeveel priemgetallen er onder de maximumgrens zijn.



