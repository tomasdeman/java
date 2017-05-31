## JavaFx: inleiding

JavaFX is een Java bibliotheek met als doel een grafische user interfaces \(GUI\) te laten ontwerpen. Als je in IntelliJ IDEA een JavaFX programma maakt, bestaat dit uit 3 bestanden:

* de Main klasse: hier start je programma en wordt je fxml bestand gekoppeld aan de Controller klasse. Hier kan je bijvoorbeeld
* het fxml bestand: dit bestand beschrijft de layout van je venster. Dit kan je d.m.v. een rechtermuisklik bewerken in de Scene Builder.
* de Controller klasse: hierin doe je alle interactie met je Controls. Als er op een `Button` geklikt wordt of als er een Label van tekst met veranderen doe je dit hier. TIP: ontwerp eerst alle hulpklassen, zodat je deze vanuit je Controller kan gebruiken.

Hieronder een overzicht van de te gebruiken controls. Zoek gerust in de documentatie van JavaFX \([https://docs.oracle.com/javase/8/javafx/api/toc.htm](https://docs.oracle.com/javase/8/javafx/api/toc.htm)\) welke methoden je zal moeten gebruiken voor het probleem dat je wil oplossen.

### Container controls

Container controls dienen om ander controls in te stoppen. Je kan ook een container in een andere container stoppen.  
Welke containers gebruiken we?

* `AnchorPane`: de eenvoudigst te gebruiken control, aangezien alle controls die je hierin stopt blijven staan op de bedoelde plaats.
* `HBox` en `VBox`: dient om automatisch de bevatte controls naast of onder elkaar te schikken. Met padding en spacing kan je witruimte voorzien.
* `GridPane`: een raster waarin je het aander rijen en kolommen kan bepalen. Elke cel dient dan weer als container. Vensters waarin alles in tabelvorm geschikt staat, zullen vaak GridPanes gebruiken.

### Standard Controls

* `Button`: als je hierop klikt, moet de methode gespecifiëerd bij on Action uitgevoerd worden. Met `getText()` kan je de tekst op de knop als String opvragen, met `setText(String value)` kan je de tekst opnieuw instellen.
* `Combobox`: een keuzelijst. Specifier in de controller klasse het type variabelen \(tussen &lt; en &gt;\) waarmee deze lijst gevuld is.

  ```java
  public ComboBox<Integer> leeftijden;
  ```

  Een item aan een ComboBoxtoevoegen doe je zo:  
  `combobox.getItems().add(5); //igv. een Integer ComboBox   
   combobox.getItems().add(5); //igv. een String`  


  Het juiste item selecteren doe je als volgt:

  ```java
  combobox.getSelectionModel().select(3); //selecteer het item met index 3
  combobox.getSelectionModel().select("Tomas"); //selecteer het String object met waarde "Tomas"
  combobox.getSelectionModel().selectFirst(); //selecteert het eerste item.
  ```

  Net zoals bij een Button kan je met on Action kiezen welke void methode opgeroepen moet worden in de Controller klasse als je een item selecteert.

* 


