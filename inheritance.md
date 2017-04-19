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

Momenteel hebben we dus twee klassen `PetMaster` en `Pet` . `Pet` respresenteert de eigenschappen en gedragingen van een huisdier en `PetMaster` start het programma, maakt een `Pet` aan en de methodes van dit huisdier aan.

Laten we een klasse `Fish` maken die alle eigenschappen en gedragingen van een `Pet` overneemt \(overerft\).



