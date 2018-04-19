## Overerving

Laten we starten met een klasse Pet. Deze moet kunnen eten, slapen en praten.

```java
public class Pet {

    int age;
    float weight;
    float height;
    String color;

    public void sleep(){
        System.out.println("Slaapwel!");
    }

    public void eat(){
        System.out.println("Zo een honger! Laat ik snel wat nachos eten!");
    }

    public String talk(String word){
        String petResponse = "OK!! OK!! " + word;
        return petResponse;
    }
}
```

![](/assets/friendlymonster1.png)

De methodes zoals `public void sleep()` en `public void eat()` printen een boodschap op de terminal. Aangezien deze methodes geen parameters hebben, gaan deze altijd eenzelfde gedrag simuleren.

De methode `public String talk(String word)` heeft wel een parameter _word_ en zal afhankelijk van deze parameter een ander tekst genereren. Deze wordt niet op de terminal geschreven, maar als `String` geretourneerd. Deze wordt dus aangeboden aan de klasse die deze methode oproept.

Laten we een klasse `PetMaster` maken die dit doet. Als we deze klasse ook de methode main toekennen, kunnen we dit als start van ons project nemen.

```java
public class PetMaster {

    public static void main(String[] args) {
        String petReaction;
        Pet myPet = new Pet();
        myPet.eat();
        petReaction = myPet.talk("Tweet!! Tweet!!");
        System.out.println(petReaction);
        myPet.sleep();
    }

}
```

Als we van deze klasse de main methode oproepen, zal het beestje eerst eten, dan spreken en uiteindelijk slapen.

We kunnen dus volgende output verwachten:

_Zo een honger! Laat ik snel wat nachos eten!  
Ok! Ok! Tweet! Tweet!  
Slaapwel!_

### Subklassen en superklassen

Momenteel hebben we dus twee klassen `PetMaster` en `Pet` . `Pet` respresenteert de eigenschappen en gedragingen van een huisdier en `PetMaster` start het programma, maakt een `Pet` aan en roept enkele methodes van dit huisdier aan.

Laten we een klasse `Fish` maken die alle eigenschappen en gedragingen van een `Pet` overneemt \(overerft\). Met het keyword `extends` kunnen we dit aan Java duidelijk maken.

```java
class Fish extends Pet{

}
```

`Fish` is nu een subklasse van `Pet` en `Pet` de superklasse van `Fish`.

Elke vis is een huisdier, maar niet elk huisdier een vis! Aangezien een vis een huisdier is, kunnen we elke public `Pet`-methode gebruiken zonder deze opnieuw te moeten definiëren.![](/assets/classhierarchy.png)

Nu kunnen we extra functionaliteit aan een vis geven.

```java
public class Fish extends Pet {

   int currentDepth = 0;

   public int dive(int howDeep){

    currentDepth = currentDepth + howDeep;
    System.out.println("We duiken " + howDeep + "m.");
    System.out.println("We zitten nu " + currentDepth + "m onder de zeespiegel");

    return currentDepth;
  }
}
```

Laten we nu een nieuwe klasse `FishMaster` maken.

```java
public class FishMaster {

  public static void main(String[] args) {

    Fish myFish = new Fish();

    myFish.dive(2);
    myFish.dive(3);

    myFish.sleep();
  }
}
```

Als output krijgen we nu:

_We duiken 2m.  
We zitten nu 2m onder de zeespiegel.  
We duiken 3m.  
We zitten nu 5m onder de zeespiegel.  
Slaapwel!_

### Method overriding

Het kan zijn dat je bepaalde methodes wil "overschrijven" met nieuwe functionaliteit. Neem nu de `talk()` methode. Aangezien een vis niet kan praten, zullen we deze voor de `Fish` klasse overschrijven of overriden.

In de `Fish` klasse voegen we nu volgende methode toe:

```java
public String talk(String something){
  return "Wist je dat vissen niet kunnen praten?";
}
```

Als we nu in de `FishMaster` klasse volgende code toevoegen, krijgen we een ander gedrag.

```java
String fishReaction;
fishReaction = myFish.talk("Hello");
System.out.println(fishReaction);
```

Als je dit programma uitvoert krijg je _Wist je dat vissen niet kunnen praten?_ als output.

De methode `talk()` uit de `Pet` klasse wordt volledig genegeerd! Als je wil dat beide uitgevoerd worden, kan je met het keyword `super` het object van de superklasse verwijzen. Net zoals `this` naar het huidige object verwijst.

```java
public String talk(String something){
  super.talk(something);
  return "Wist je dat vissen niet kunnen praten?";
}
```

### Abstracte klassen

De superklasse `Pet` hoeft in feite nooit geïnstantieerd te worden. Er zullen alleen subklasses gecreëerd worden \(`Fish`, `Dog`, ...\). Als je wel zou willen dat er dat de superklasse specifieert welke methodes moeten overgeërfd worden, zonder deze effectief uit te werken, kunnen we de superklasse abstract maken.

```java
abstract class Pet {
    public abstract void dance();
    public abstract void run();
}
```

Zoals je ziet bevatten deze methodes nog geen code. Deze zullen verplicht worden om in de subklassen te implementeren.

Je kan ook bepaalde methodes implementeren in de superklasse en andere abstract maken.

```java
public abstract class AbstractClass
{
    abstract public void abstractMethod();

    public void implementedMethod() { 
        System.out.print("implementedMethod()"); 
    }
}
```

Aangezien `abstractMethod()` geen body heeft, kan je het volgende niet doen:

```java
public class ImplementingClass extends AbstractClass
{
    // ERROR!
}
```

De Java Virtual Machine kan niet weten in bovenstaand voorbeeld wat te doen bij  
`new ImplementingClass().abstractMethod()`. Een abstracte methode moet geïmplementeerd worden in de subklassen.

Dit is een voorbeeld van een correcte subklasse:

```java
public class ImplementingClass extends AbstractClass
{
    public void abstractMethod() { 
        System.out.print("abstractMethod()"); 
    }
}
```

Aangezien `implementedMethod()` reeds in `AbstractClass` gedefiniëerd was, hoef je deze niet opnieuw te definiëren. Maar je kan die natuurlijk wel overriden.

```java
public class ImplementingClass extends AbstractClass
{
    public void abstractMethod() { 
        System.out.print("abstractMethod()"); 
    }

    public void implementedMethod() { 
        System.out.print("Overridden!"); 
    }
}
```

### De `instanceof` operator

Java heeft een binaire operator `instanceof` die een boolean waarde teruggeeft. Als het object een instantie van de klasse is, geeft deze operator true terug, anders false.

Zo kan je bijvoorbeeld nagaan welk type Pet een bepaald object is. In onderstaande code overlopen we de `ArrayList` en laten we alle niet-vissen spreken.

```java
ArrayList<Pet> list = new ArrayList<>();
list.add(new Fish());
list.add(new Horse());
list.add(new Fish());
list.add(new Dog());
list.add(new Fish());

for (Pet p : list) {
    if (!(p instanceof Fish)) {
        System.out.println(p.talk("Hellooo!"));
    }
}
```

### De factory pattern

Als je objecten wil creëren van subklassen van eenzelfde superklasse, wordt er vaak gebruik gemaakt van het zogenaamde factory pattern. Hierbij maak je een klasse dat met een enkele methode elk gewenst object van één van de subklassen kan aanmaken.

```java
public class PetFactory {

   public Pet getPet(String petType){
      if(petType.equalsIgnoreCase("FISH")){
         return new Fish();

      } else if(petType.equalsIgnoreCase("DOG")){
         return new Dog();

      } else if(petType.equalsIgnoreCase("CANARY")){
         return new Canary();
      }

      return null;
   }  

}
```

Zo kan je in je `Main` klasse een `PetFactory` aanmaken en deze al het werk laten doen.

```java
public class Main {
   public static void main(String[] args) {
      PetFactory petFactory = new PetFactory();

      //get an object of Fish and call its dance method.
      Pet pet1 = petFactory.getPet("FISH");
      pet1.dance();

      //get an object of Dog and call its dance method.
      Pet pet2 = petFactory.getPet("DOG");
      pet2.dance();

      //get an object of Canary and call its dance method.
      Pet pet3 = petFactory.getPet("CANARY");
      pet3.dance();
   }
}
```

### Oefening 1: Game

In een `Game` zitten verschillende vijanden: _Trollen_ en _Draken_.

Merk op dat de `Trol` klasse en de `Draak` klasse enige overeenkomsten vertonen!  
Dus maken we een bovenklasse\(of superklasse\) `Vijand`.

#### 1. De klasse `Vijand`

Deze klasse bevat alle gemeenschappelijke variabelen en methodes van `Draak` en `Trol`.  
Denk goed na welke elementen in deze beide klassen voorkomen en plaats deze dan in de klasse `Vijand`. Geef elke vijand op zijn minst een naam en een voornaam.

#### 2. De klasse `Draak`

Deze klasse bevat elementen die specifiek voor de draak zijn.

Bijvoorbeeld:

* Kleur
* Vleugelbreedte
* Radius

Voorzie de nodige getters en setters.  
Voorzie ook een methode `spuwVuur()` die afdrukt dat de draak aanvalt: gebruik de specifieke voor en achternaam van de bewuste draak \(bv. "Smaug De Verschrikkelijke valt aan"\) en dat iedereen in een straal van radius geroosterd is \(bv. Iedereen in de straal van 4 km is geroosterd\).

**MERK OP:**

De methoden in de bovenklasse komen hier ook automatisch terecht \(ze worden overgeërfd\). Je kan dus gewoon methodes gebruiken van de bovenklasse alsof ze in deze klasse zouden staan.

#### 3. De klasse `Trol`

Deze klasse bevat elementen die specifiek voor de Trol zijn.

Bijvoorbeeld:

* Grootte
* Snelheid

Voorzie de nodige getters en setters.

Voorzie ook een methode `slaMetKnots(int knotsGrootte)` die afdrukt dat iedereen boem baf doodgemept is. Let op! Als de knots groter is dan de `Trol` zelf, dan wordt er afgedrukt dat hij zijn knots niet kan dragen.

Druk ook de naam af van de trol in beide gevallen.

**MERK OP:**

De methoden in de bovenklasse komen hier ook automatisch terecht \(ze worden overgeërfd\). Je kan dus gewoon methodes gebruiken van de bovenklasse alsof ze in deze klasse zouden staan.

#### 4. De klasse `Game`

Hier worden de vijanden bijgehouden. Gebruiken we een array of een `ArrayList`?

Voorzie een methode `voegVijandToe(Vijand v)` die een vijand toevoegt.

Voorzie een methode `printVijanden()` die alle vijanden in het spel afdrukt.

Voorzie een methode `printDraken()` die alle draken in het spel afdrukt.

Voorzie een methode `valAanVijanden()` waarin alle vijanden gaan aanvallen. Aanvallen wil zeggen:

1. Als het een `Trol` is, wordt `slaMetKnots` opgeroepen \(je kan zelf kiezen hoe groot de knots is\)
2. Als het een `Draak` is, wordt `spuwVuur` opgeroepen

Oplossing: [Solutions/Game.zip](Solutions/Game.zip)

### Oefening 2: shapes

Maak een Java project dat wiskundige figuren aanmaakt en beheert. Voorzie op zijn minst een rechthoek, een cirkel, een vierkant, een driehoek en een ovaal.

Elke figuur moet zijn oppervlakte en omtrek kunnen berekenen en teruggeven. Ook moet een elke `Shape` een `print()` methode hebben die het type object op de terminal afdrukt en de details over de figuur \(omtrek, oppervlakte, zijde x, radius, ...\).

Als de constructor aangeroepen wordt van een figuur zonder parameters, vul je deze willekeurig in.

Maak ook een `ShapeFactory` die een shape kan aanmaken van elke gewenste vorm, zowel random als bepaald.

In de hoofdklasse `ShapesSimulation` maak je dan de `ShapeFactory` aan. D.m.v. een `for`-lus laat je deze dan een aantal random figuren aanmaken en in een `ArrayList` stoppen.

Voorzie ook volgende methodes:

* `printTriangles()`
* `printAllShapes()`
* `printCircles()`
* `printTotals()` : deze methode print de totale omtrek en oppervlakte van alle figuren af.



