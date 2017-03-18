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

  ![](/assets/nv.png)

* * \(Merk op dat je een normaalverdeling krijgt\)

  * Uitbreiding \(eventueel\): In plaats van de output op de terminal te doen met System.out.println\(\), zou je de normaalverdeling op een grafiek kunnen zetten met een JavaFX barChart. Zoek online op hoe je deze kan gebruiken \(bvb. op [https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm) \).

Oefening 2: Zeef van Eratosthenes

```
Dit is een algoritme waarmee je priemgetallen kan bepalen tot aan een zekere bovengrens.

In deze methode creëer je een array van booleans \(priem\). 
Je zet eerst alle elementen op True, en daarna zal je, via onderstaand algoritme, alle niet‐priemgetallen schrappen. 
Daarna druk je deze getallen ook af \(10 per lijn\)

Wil je bijvoorbeeld de priemgetallen bepalen tot aan 1000, dan ga je als volgt te werk:
Schrijf alle getallen van 2 tot 1000 op.
Schrap alle veelvouden van 2.
Het eerstvolgende getal dat nog niet geschrapt is, is 3. Schrap nu alle veelvouden van 3.
Het eerstvolgende getal dat nog niet geschrapt is, is 5. Schrap nu alle veelvouden van 5.
Door deze methode voldoende lang vol te houden vind je alle priemgetallen tussen 0 en 1000.
Als scherm‐output moet je ongeveer onderstaande bekomen:
```



