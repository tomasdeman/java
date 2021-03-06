## Arrays

Een concept waar iedere programmeur dient mee vertrouwd te zijn is een array.

### Wat is een array?

Een "standaard" variabele kan een waarde opslaan, maar dan ook slechts één waarde.  
Een array kan daarentegen een hele lijst van waardes van hetzelfde type opslaan, zowel primitieve types \(int, double, ...\) als objecten. Je kan dus evengoed een array van `int` waardes opslaan als van objecten van de klasse `Persoon`.

Arrays zijn eenvoudig te declareren door vierkante haken te gebruiken. Je kan kiezen of je deze na de typenaam of na de variabelenaam zet.

De declaratie van een arrayvariabele is herkenbaar aan een paar vierkante haken die volgen op de typenaam of variabelenaam.

```java
private int[] uurteller; 
private int uurteller[];
private int[] coeff;
```

Dit geeft aan dat beide variabelen van het type integer array zijn. We zeggen dat het _basistype_ van deze arrays `int` is.

De variabele `teller` kan één geheel getal bevatten, de variabele `uurteller` verwijst naar een arrayobject zodra dat object gemaakt is. Door het declareren van de arrayvariabele wordt het arrayobject nog niet aangemaakt. Dat gebeurt pas met behulp van de operator new \(zoals bij andere objecten\).

Nog enkele voorbeelden:

```java
float temperaturen [];
double[] meetwaarden;
byte getallen[];
String namen[];
char letters[];
boolean priem[];
```

Een array heeft steeds een vaste lengte die bij initialisatie bepaald wordt.  
Initialiseren kan op twee manieren: je kan direct de waarden meegeven tussen accolades, gescheiden door komma's, of je kan de array leeg laten.  
Hier zie je ook dat we met de `new` operator de array aanmaken.

```java
namen = new String[] {"Filips", "Adams", "Declercq"};
klinkers = new Char[] {'a', 'e', 'i', 'o', 'u'};
priem = new boolean[1000];
maanden = new double[12];
coeff = new int[10];
```

De afzonderlijke elementen van een array worden benaderd door gebruik te maken van een index. Bijvoorbeeld: `label[6]` of `coeff[3]` .  
In bovenstaand voorbeeld bevat de array namen drie elementen.  
Het element `namen[0]` bevat `"Filips"`, `namen[1]` bevat `"Adams"` en `namen[2]` bevat `"Declercq"`.  
De index \(tussen de vierkante haken\) is een integerexpressie. De geldige waarden hiervoor zijn afhankelijk van de array waarvoor ze worden gebruikt.

**Let op: indexnummers beginnen altijd bij 0 \(nul\) en lopen tot één minder dan de lengte van de array.**

### De for-lus

De `for`-lus wordt gebruik om:

* een stukje code een vooraf bepaald aantal keer te laten uitvoeren en
* een variabele binnen de lus te hebben waarvan de waarde elke keer een regelmatig aantal verandert \(meestal +1 bij elke iteratie\) 

De algemene vorm van de `for`-lus is:

```
for (initialisering; conditie; actie na de body) { 
    te herhalen opdrachten 
}
```

Bijvoorbeeld:

```java
for (int teller = 0; teller < coeff.length; teller++){ 
    System.out.println(teller + “:” + coeff[teller]);
}
```

Alle arrays bevatten een veld `length` dat de waarde van de onveranderlijke omvang van de array bevat.  
Deze waarde komt overeen met de waarde van de integerexpressie die gebruikt werd om het arrayobject te creëren.  
Bij `coeff` is dit 10: de indices lopen dus van 0 tot 9.

Je kan ook een `for`-lus binnen een `for`-lus gebruiken, een herhaling binnen een herhaling als het ware. Een typisch voorbeeld is het tekenen van een rechthoek, al dan niet gevuld. Deze wordt dan vanuit de `main` methode in de klasse `Main` aangeroepen.

```java
public class Rechthoek {

    public void tekenRechthoek(int breedte, int hoogte, boolean gevuld) {

        if (!gevuld) {
            for (int h = 1; h <= hoogte; h++) {
                if (h == 1 || h == hoogte) {
                    for (int b = 1; b <= breedte; b++) {
                        System.out.print("*");
                    }
                    System.out.println("");
                } else {
                    System.out.print("*");
                    for (int b = 1; b <= breedte - 2; b++) {
                        System.out.print(" ");
                    }

                    System.out.println("*");
                }
            }
        } else {
            for (int h = 1; h <= hoogte; h++) {
                for (int b = 1; b <= breedte; b++) {
                    System.out.print("*");
                }
                System.out.println("");
            }
        }
    }
}
```

De klasse `Main` kan er dan zo uitzien:

```java
public class Main {

    public static void main(String[] args) {

        Rechthoek r = new Rechthoek();
        r.tekenRechthoek(50, 6, true);

    }
}
```

Als output krijg je dan:

```
**************************************************
**************************************************
**************************************************
**************************************************
**************************************************
**************************************************
```

Ook grote sommen zijn makkelijk met lussen te berekenen. Wil je bijvoorbeeld een methode maken die de som maakt van alle integers tussen twee getallen. Dan kan je gewoon een teller laten lopen van het kleinste tot en met het grootste getal en deze steeds bij een variabele som optellen.

```java
public int somGetallen(int min, int max) {
    int som = 0;
    for (int i = min; i <= max; i++) {
        som += i;
    }
    return som;
}
```

Ook voor wiskundige rijen zijn vaak lussen een oplossing om een titanenwerk te vermijden. Neem nu bijvoorbeeld de reeks van Fibonnaci. Hierbij zijn de eerste twee getallen reeds gegeven \(0 en 1\). De volgende getallen kan je eenvoudig laten berekenen door een algoritme.

```java
public int[] fibonnaci(int count) {

    int row[] = new int[count];

    row[0] = 0;
    row[1] = 1;

    for (int i = 2; i < count; i++) {
        row[i] = row[i-1] + row[i-2];
    }

    return row;

}
```

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
    * declareert en genereert een random generator
    * initialiseert de `array` ogen en simuleert het gooien
  * `toonResultaat()`: toont van elk aantal ogen hoeveel keer het gegooid werd.

    Het resultaat kan er als volgt uitzien:

  ```
  Simulatie: 100 keer gooien met 3 dobbelstenen leverde volgende sommen op
  3 : 0 keer gegooid.
  4 : 2 keer gegooid.
  5 : 0 keer gegooid.
  6 : 3 keer gegooid.
  7 : 9 keer gegooid.
  8 : 18 keer gegooid.
  9 : 13 keer gegooid.
  10 : 8 keer gegooid.
  11 : 15 keer gegooid.
  12 : 11 keer gegooid.
  13 : 7 keer gegooid.
  14 : 4 keer gegooid.
  15 : 2 keer gegooid.
  16 : 6 keer gegooid.
  17 : 2 keer gegooid.
  18 : 0 keer gegooid.
  ```

  Merk op dat je een normaalverdeling krijgt.

#### Uitbreiding 1:

In plaats van de output op de terminal te zetten met `System.out.println()`, zou je de normaalverdeling op een grafiek kunnen zetten met een _JavaFX_ `barChart`.  
Zoek online op hoe je deze kan gebruiken. Enkele voorbeelden van pagina's die je hierbij helpen:

* [https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm](https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/bar-chart.htm)
* [http://www.java2s.com/Tutorials/Java/JavaFX/0850\_\_JavaFX\_BarChart.htm](http://www.java2s.com/Tutorials/Java/JavaFX/0850__JavaFX_BarChart.htm)

#### Uitbreiding 2:

In plaats van elke simulatie met 3 dobbelstenen uit te voeren of 100 keer te gooien, zou je deze twee waardes als parameter kunnen meegeven.

### Oefening 2: Zeef van Eratosthenes

Dit is een algoritme waarmee je alle priemgetallen kan bepalen tot aan een zekere bovengrens.

Het algoritme werkt als volgt.

1. Creëer een array van booleans \(priem\). De bovengrens van deze array is het maximale getal dat je wil onderzoeken.  
   Als je dus wil weten welke priemgetallen er zijn met als maximumgrens 500, maak je een array met 501 elementen.

2. Zet alle elementen op `true`

3. Schrap als volgt alle niet-priemgetallen in de array door ze op `false` te zetten:

   1. Zet de eerste twee indexen van de array `priem` op false. We weten namelijk dat 0 en 1 geen priemgetallen zijn.

   2. Als je een priemgetal tegenkomt, moet je in de array `priem` alle veelvouden van dit priemgetal schrappen. Dit doe je door steeds een nieuwe for-lus te starten bij elk priemgetal je tegenkomt. Je kan dit eventueel met behulp van een andere methode doen.

   3. Als je buitenste lus het maximum bereikt heeft, heb je alle priemgetallen gevonden.

4. Druk deze getallen af op de terminal \(10 per lijn\).

Wil je bijvoorbeeld de priemgetallen bepalen tot aan 1000, dan ga je als volgt te werk:

* Schrijf alle getallen van 2 tot 1000 op.
* Schrap alle veelvouden van 2.
* Het eerstvolgende getal dat nog niet geschrapt is, is 3. Schrap nu alle veelvouden van 3.
* Het eerstvolgende getal dat nog niet geschrapt is, is 5. Schrap nu alle veelvouden van 5.
* Door deze methode voldoende lang vol te houden vind je alle priemgetallen tussen 0 en 1000.

```
De priemgetallen met als maximumgrens 1000 zijn:
2 3 5 7 11 13 17 19 23 29 
31 37 41 43 47 53 59 61 67 71 
73 79 83 89 97 101 103 107 109 113 
127 131 137 139 149 151 157 163 167 173 
179 181 191 193 197 199 211 223 227 229 
233 239 241 251 257 263 269 271 277 281 
283 293 307 311 313 317 331 337 347 349 
353 359 367 373 379 383 389 397 401 409 
419 421 431 433 439 443 449 457 461 463 
467 479 487 491 499 503 509 521 523 541 
547 557 563 569 571 577 587 593 599 601 
607 613 617 619 631 641 643 647 653 659 
661 673 677 683 691 701 709 719 727 733 
739 743 751 757 761 769 773 787 797 809 
811 821 823 827 829 839 853 857 859 863 
877 881 883 887 907 911 919 929 937 941 
947 953 967 971 977 983 991 997
```

#### Uitdaging:

houd bij hoeveel priemgetallen er onder de maximumgrens zijn. Maak dus een methode `countPrimes` die het aantal priemgetallen onder een maximumgrens kan berekenen.

### Oefening 3: tafels

Maak een programma dat op je terminal de tafels van x afdrukt. Als je dit programma uitvoert voor de tafels van 10, zou je volgende output bekomen:

```
De tafels van 10
1 * 10 = 10
2 * 10 = 20
3 * 10 = 30
4 * 10 = 40
5 * 10 = 50
6 * 10 = 60
7 * 10 = 70
8 * 10 = 80
9 * 10 = 90
10 * 10 = 100
```

### Oefening 4: mediaan

Maak een methode die de mediaan berekent van een array met double getallen.

Vul de array eerst met random double waardes. Om de mediaan te kunnen berekenen zal je deze eerst moeten sorteren. Dit kan je doen met `Arrays.sort(array)`.

Druk zowel de waardes af als de mediaan.

[Solutions/eratosthenes.zip](Solutions/eratosthenes.zip) [Solutions/Dobbelen.zip](Solutions/Dobbelen.zip)

