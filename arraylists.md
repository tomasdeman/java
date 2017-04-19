## ArrayLists

Arrays zijn enorm handig om lijsten bij te houden, maar zo biedt Java nog enkele structuren.  
Arrays hebben ook nadelen t.o.v. bijvoorbeeld ArrayLists. Hieronder enkele verschillen tussen arrays en ArrayLists:

#### 1. Aanmaken van de lijst

```java
ArrayList<String> notes;
notes = new ArrayList<String>();
```

![](/assets/import.png)

#### 2. Grootte

Eenmaal de array aangemaakt is is de grootte ervan onveranderlijk. Je moet m.a.w. op voorhand bepalen hoe groot je array moet zijn. Een `ArrayList` daarentegen kan dynamisch groeien of krimpen.

#### 3. Het aantal elementen opvragen

Bij een array vroeg je het aantal elementen op met de eigenschap `length`. Bij een ArrayList gebruik je hiervoor de `size()` methode.

#### 4. Type elementen

In een `ArrayList` kan je alleen objecten opslaan en dus geen primitieve waardes. Dit kan dan wel weer met een array.

Deze kunnen echter d.m.v. _autoboxing_ geconverteerd worden naar een object, zodat het lijkt alsof je toch een primitief kan opslaan in een `ArrayList`. Dit zou dan als volgt kunnen:

```java
ArrayList<Integer> integerList = new ArrayList<Integer>();
integerList.add(1); 
//in realiteit wordt niet de int waarde 1 in de ArrayList gestopt, maar via een systeem van
//autoboxing
```

#### 5. Een element aan de lijst toevoegen

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

#### 6. Een element uit de lijst verwijderen

Bij een array kan dit niet. De lijst blijft steeds even groot. Je kan echter het element de waarde null geven.  
Bij een ArrayList kan je wel een element met de remove\(\) methode verwijderen. Als parameter geef je de positie of index mee, te beginnen met 0.

De lijst bevat dan effectief een element minder.

```java
lijstStudenten.remove(0);
```

#### 7. De lijst doorlopen en een element opvragen

Een array met objecten doorloop je meestal met een `for`-lus. Een voorbeeldje met `String` objecten:

```java
String[] namen = {"Bob", "Jan", "Bert", "An", "Lars", "Els", "Alissa"};
for (int i = 0; i < namen.length; i++) {
    System.out.println("Hallo, " + namen[i]);
}
```

Een ArrayList kan dan weer op volgende twee manieren doorlopen:

```java
//Maak een iterator (teller) die je als index gebruikt
for (int i = 0; i < stringList.size(); i++) {
 String item = stringList.get(i);
 System.out.println("Item " + i + " : " + item);
}

//Of gebruik een for each lus
for(String item: stringList){
 System.out.println("Element: " + item);
}
```

## Samenvatting

| ArrayList&lt;Type&gt; |  |
| :--- | :--- |
| `public ArrayList<Type>()` | Constructor |
| `public void add (Type element);` | Toevoegen van een element |
| `public void remove (int index)` | Verwijderen van een element \(0 &lt;= index &lt; size\(\)\) |
| `public Type get (int index)` | Opvragen van een element \(0 &lt;= index &lt; size\(\)\) |
| `public int size()` | Opvragenvan degrootte van deArrayList |



