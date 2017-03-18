# Project Hangman

## STAP 1: Project Management

Maak een account aan op [Trello.com](http://www.trello.com). Hier kan je per project een nieuw bord aanmaken.  
Maak hierop het Bord “Java: Hangman” aan.

In elk project dat we met Trello willen managen, maken we vier kaarten aan: Backlog, TODO, WIP \(work in progress\), DONE.

Initiëel plaats je al je ideeën op de backlog kaart, hoe vergezocht deze ook mogen lijken. In het geval van een software project maak je hier een user story van \(x moet y kunnen zodat z\).

Daarna overloop je welke user stories noodzakelijk zijn om je project als geslaagd te beschouwen. We noemen dat het MVP \(Minimum Viable Project\). Deze ideeën verplaats je naar de TODO kaart.  
Je kiest dan een idee van TODO dat je gaat implementeren en sleept dit naar WIP.  
Als het volledig af is, kan je dit bij DONE zetten.

Hieronder vind je de functionaliteit die minimaal \(=MVP\) nodig is om Hangman te kunnen spelen. Soms heb ik in de oplossing verschillende functionaliteiten tegelijk opgelost. Test elk stukje code je schrijft direct, zodat je niet op het einde alle fouten moet debuggen!

![](/assets/import.png)

## STAP 2: Als rader moet ik een letter kunnen ingeven, zodat ik het spel kan spelen

Je moet beslissen op welke manier je door de gebruiker een letter laat ingeven.

Enkele opties:

1. Je kan een `TextField` maken met een knop naast. Welke voor- en nadelen zijn hieraan verbonden?
2. Je kan een `ComboBox` gebruiken. Welke voor- en nadelen zijn hieraan verbonden?
3. Je kan een volledig toetsenbord creëren met `Button` objecten. Welke voor- en nadelen zijn hieraan verbonden?
4. Je kan zelfs een `KeyListener` implementeren die als het ware luistert of er een toets wordt ingedrukt en hier dan op reageert. Welke voor- en nadelen zijn hieraan verbonden?
5. …

Kies momenteel voor een invoermethode die je reeds kan implementeren en toch zo duidelijk mogelijk is.

Ik koos voor methode 3. Uiteraard mag jij ook een andere methode kiezen.

![](/assets/implementation.png)

Voor het JavaFX toetsenbord werk ik met verschillende containers:

* Een rij `Button` objecten maak je door verschillende Buttons in een `HBox` container te stoppen. Hiervoor maak je best 1 `Button`, laat je zijn on action gebeurtenis wijzen naar een zelfgekozen methode \(bvb. `buttonPressed`\) uit de Controller klasse \(bvb `sample`.`Controller` of een eigen gekozen package/klasse combinatie\). Je kan al je `Button` objecten naar deze zelfde methode laten verwijzen, dus je kan deze gewoon dupliceren.
* Ook kan je nu je eerste `Hbox` dupliceren om een nieuwe rij te maken.  Daarna stop je al je `HBox` containers in een `VBox`  om deze onder elkaar te plaatsen.
* Controleer in al je containers de spatiëring \(Padding en Spacing bij Layout\).

![](/assets/spacing.png)

* Laat ook de Preferred Width en Height door de computer berekenen.
* Als al je `Button` objecten op de `Scene` staan, druk je op _CTRL-S_ \(opslaan\) en ga je in IntelliJ IDEA naar je _.fxml_ bestand. Normaalgezien staan daar 26 verwijzingen in het rood gemarkeerd, omdat de void methode `buttonPressed` in de Controller waar de Buttons naar verwijzen niet bestaat.
* Ga op één van de rode verwijzingen staan en druk op _ALT-ENTER_.
* Laat IDEA de methode creëren in de `Controller` class.

![](/assets/createmethod.png)

* Sla je _.fxml_ bestand op en ga naar de `Controller` class waar we de methode zullen testen.
* Om te testen of dit volstaat om een letter in te voeren, kunnen we deze op de terminal afdrukken als `String`.
* Je methode in de `Controller` class heeft een `ActionEvent` als parameter. Deze bevat informatie over hoe deze methode opgeroepen is. We willen eerst aan een verwijzing naar de juiste `Button` geraken met `actionEvent.getSource()  getSource()`geeft een object van het type `Object`. We moeten deze nog casten \(=omzetten\) naar een `Button`. Dan kunnen we met `getText()` de letter die erop staat uitlezen.

```java
public void buttonPressed(ActionEvent actionEvent) {  
    Button b = (Button)actionEvent.getSource(); 
    System.out.println(b.getText()); 
}
```

* * Nu hebben we onze eerste User Story afgewerkt en kunnen we deze naar WIP verplaatsen.

## STAP 3: Als rader zou ik mijn vooruitgang moeten kunnen zien, zodat ik een beredeneerde gok kan doen.

De toestand van het spel en de methodes om een gok te doen, stop je best in een aparte nieuwe klasse `Game` zodat de spellogica volledig gescheiden is van de layout of GUI \(Graphical User Interface\).

De `Controller` klasse kan dan de nodige methodes in de `Game` klasse aanroepen waar nodig.  
 Als we ooit onze `Scene` willen veranderen en bijgevolg onze `Controller` willen wijzigen, kan dat dan zonder iets aan de `Game` class te moeten veranderen.

De `Game` class houdt het juiste antwoord bij, alsook een `private String` met de missers en een `String` met de hits. Maak hier dan getter functies \(accessoren\) voor.

In de constructor geef je als parameter het antwoord mee. Eventueel zet je hier het antwoord om naar hoofdletters zodat je niet op kleine letters moet controleren. Ook initialiseer je hier de `String` objecten hits en misses naar `""`.

Maak nu een methode `applyGuess` die als argument de gok meekrijgt:

```java
public void applyGuess(char letter) {
    …
}
```

Deze moet kijken of de letter in het antwoord voorkomt en deze ofwel aan de hits `String` toevoegen ofwel aan de misses `String`.

Uitbreiding 1: in `applyGuess` kan je zorgen dat een letter alleen aan de hits of misses `String` wordt toegevoegd, als hij er nog niet inzat.

Uitbreiding 2: maak een methode `triesLeft` die als `int` teruggeeft hoeveel beurten er nog zijn. Je kan deze methode dan gebruiken in `applyGuess` om alleen de letter toe te voegen als er nog beurten over waren.

Zorg nu in de `Controller` dat, als er een letterknop ingedrukt wordt, deze aan de game meegegeven wordt d.m.v. de `applyGuess` methode. Zo is je Game up-to-date.

Maak in de scene builder alle `Label` objecten \(`fx:id` -&gt; hits, misses, triesLeft, progress\) aan. Zie eventueel screenshot op pagina 2.

Maak in je `Controller` class ook een methode `fillLabels` die alle `Label` objecten updatet met de huidige waarde uit het `Game` object game. Het progress `Label` doen we hierna.

```java
private void fillLabels() {	
    misses.setText("Fouten: " + game.getMisses());
    hits.setText("Juist: " + game.getHits());
    triesLeft.setText("Levens: " + game.getTriesLeft());
}
```

Wanneer moet deze methode aangeroepen worden?

Het progress `Label` vul je door met een herhaling elke letter uit het antwoord te doorlopen en te controleren of deze al in de hits `String` aanwezig is. Als hij aanwezig is toon je de letter, anders een underscore.

Na elke letter of underscore plaats je best een spatie voor de leesbaarheid. Hierin maak ik gebruik van een `for` lus \(=herhaling\) die elke letter in het juiste antwoord overloopt.

```java
public String getProgress() {    
    String progress = "";    
    for (char letter : answer.toCharArray()) {
        char display = '_';
        if (hits.indexOf(letter) >= 0) {
            display = letter;        
        }        
        progress += display + " ";
    }
    return progress;
}
```

Vul nu in `fillLabels` ook het progress `Label` met de methode die je net gemaakt hebt.  
Test het spel en voeg functionaliteit naar wens toe!

