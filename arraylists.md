## ArrayLists

Arrays zijn enorm handig om lijsten bij te houden, maar zo biedt Java nog enkele structuren.  
Arrays hebben ook nadelen t.o.v. bijvoorbeeld ArrayLists. Hieronder enkele verschillen tussen arrays en ArrayLists:

#### 1. Grootte

Eenmaal de array aangemaakt is is de grootte ervan onveranderlijk. Je moet m.a.w. op voorhand bepalen hoe groot je array moet zijn. Een `ArrayList` daarentegen kan dynamisch groeien of krimpen.

#### 2. Het aantal elementen opvragen

Bij een array vroeg je het aantal elementen op met de eigenschap `length`. Bij een ArrayList gebruik je hiervoor de `size()` methode.

#### 3. Type elementen

In een `ArrayList` kan je alleen objecten opslaan en dus geen primitieve waardes. Dit kan dan wel weer met een array.

Deze kunnen echter d.m.v. _autoboxing_ geconverteerd worden naar een object, zodat het lijkt alsof je toch een primitief kan opslaan in een `ArrayList`. Dit zou dan als volgt kunnen:

```java
ArrayList<Integer> integerList = new ArrayList<Integer>();
integerList.add(1); 
//here we are not storing the primitive int value 1 in an ArrayList, instead autoboxing will convert 
//the int primitive to an Integer object
```

#### 4. Een element aan de lijst toevoegen

Bij een array kan je op positie i een element toewijzen door de toewijzingsoperator =, bvb:

```java
Object[] objArray = new Object[10];
objArray[1] = new Object();
```

Een element aan een ArrayList toevoegen doe je m.b.v. de add\(\) methode. Dit zou dan weer zo kunnen:

```java
ArrayList<Persoon> lijstStudenten = new ArrayList<Persoon>();
lijstStudenten.add(new Persoon("Bart", "DeSmedt", 18, "Gent"));
```

#### 5. Een element uit de lijst verwijderen

Bij een array kan dit niet. De lijst blijft steeds even groot. Je kan echter het element de waarde null geven.  
Bij een ArrayList kan je wel een element met de remove\(\) methode verwijderen. Als parameter geef je de positie of index mee, te beginnen met 0.

De lijst bevat dan effectief een element minder.

```java
lijstStudenten.remove(0);
```



