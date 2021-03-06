## Project: vier op een rij

![](/assets/c4_gui.png)

Start met een nieuw JavaFX project. Kopieer alle code die je wil, maar probeer deze steeds te begrijpen. Vraag desnoods om extra uitleg.

Soms zal code niet werken als je deze kopiëert. Dit zal waarschijnlijk gebeuren omdat deze een methode aanroept die bij jou nog niet in het programma zit. Zet deze methode dan best voorlopig in commentaar.

Bovenstaande `Scene` is deels gemaakt in de _Scene Builder_, deels via code. De zwaar repitieve stukken doen we deze keer met code.

Volgende onderdelen zijn in de _Scene Builder_ gemaakt:

* Het bord zelf is een `GridPane` van 6 rijen en 7 kolommen.
* Boven het bord staat een `GridPane` van 1 rij en 7 kolommen om de besturing te voorzien.
* Onderaan staat momenteel nog een Reset `Button`   
* Alle drie deze onderdelen zitten in een `VBox`

Je zal ongetwijfeld wat moeten sleutelen de instellingen om dit alles correct en naar smaak te verkrijgen met de _Scene Builder_.

De bovenste kleine `GridPane` heeft als fx:id `topGrid`. De `Button` objecten in deze grid zijn d.m.v. code aangemaakt om herhaling te vermijden.

De `GridPane` daaronder heet `boardGridPane`. Hierin zijn opnieuw 42 `Circle` objecten d.m.v. code in een `for`-lus aangemaakt.

 Probeer eerst de layout van beide grids goed te krijgen alvorens deze te vullen. Soms is het handig code rechtstreeks in je fxml bestand aan te passen.

Ook kan je best dezelfde bestandsnamen en packagenaam `connect4` te gebruiken als in onderstaande screenshot om de codevoorbeelden goed te begrijpen.

![](/assets/c4filenames.png)

De klasse met de main methode heet `Connect4Main`. De controller klasse heb ik `Connect4BoardGUI` genoemd.  
GUI staat voor _Graphical User Interface_.

Ook maak je best een klasse `Constants` aan met constanten. Hieronder een deel van de gebruikte constanten.

```java
package connect4;

import javafx.scene.paint.Color;

public class Constants {
    public final static Color COLOR_EMPTY = Color.GRAY;
    public final static Color COLOR_RED = Color.RED;
    public final static Color COLOR_YELLOW = Color.YELLOW;
    public final static int NOT_FOUND = -1;
}
```

De start methode in Connect4Main is gewijzigd, omdat we een verwijzing nodig hebben naar de Controller klasse. Deze verwijzing is dan `connect4BoardGUI`.

```java
public void start(Stage primaryStage) throws Exception{

        FXMLLoader fxmlLoader = new FXMLLoader(getClass().getResource("connect4.fxml"));
        Parent root = fxmlLoader.load();
        primaryStage.setTitle("4 op een rij");
        primaryStage.setScene(new Scene(root));
        primaryStage.setResizable(false);
        Connect4BoardGUI connect4BoardGUI = fxmlLoader.getController();


        primaryStage.show();


        //Connect4Game connect4Game = new Connect4Game(connect4BoardGUI, new ComputerPlayer("Tomas", COLOR_YELLOW), new ComputerPlayer("Lies", COLOR_RED));
        //connect4BoardGUI.setConnect4Game(connect4Game);
        //while(connect4Game.getCurrentPlayer() instanceof ComputerPlayer && !connect4Game.isGameFinished()) {
        //    connect4Game.checkIfComputerNeedsToMove();
        //}
        //if (connect4Game.isGameFinished()) {
        //    connect4BoardGUI.getEval().printBoard();
        //    boolean b = connect4Game.isGameFinished();
        //    System.out.println("Finished!");
        //}

}
```

### Connect4BoardGUI

Start nu met het uitwerken van de User Interface \(GUI\).

De kolommen en rijen uit de `GridPane` objecten kan je centreren met volgende methodes:

```java
private void centerColumns() {
    for (int col = 0; col < getNumberOfColumns(); col++) {
        boardGridPane.getColumnConstraints().get(col).setHalignment(HPos.CENTER);
        topGrid.getColumnConstraints().get(col).setHalignment(HPos.CENTER);
    }
}

private void centerRows() {
    for (int row = 0; row < getNumberOfRows(); row++) {
        boardGridPane.getRowConstraints().get(row).setValignment(VPos.CENTER);
    }
    topGrid.getRowConstraints().get(0).setValignment(VPos.CENTER);
}
```

In elke GridCell staat er een grijs `Circle` object. Als er een rode of gele schijf moet in belanden verander je gewoon de bewuste `Circle` van kleur. Op het moment dat de Circle gemaakt wordt, geef ik die een identiteit mee. Ook hiervoor maak je best een aparte functie.

```java
for (int row = 0; row < getNumberOfRows(); row++) {
    for (int col = 0; col < getNumberOfColumns(); col++) {
        Circle c = new Circle(40, COLOR_EMPTY);
        c.setId(makeId(col, row));
        boardGridPane.add(c, col, row);
    }
}
```

```java
private String makeId(int row, int col) {
    String s = "c" + col + ",r" + row;
    return s;
}
```

Ook de Button objecten voeg je op een dergelijke manier toe aan de bovenste grid.

```java
for (int col = 0; col < getNumberOfColumns(); col++) {
    Button b = new Button(String.valueOf(col + 1));
    b.setOnAction((event) -> {
        buttonClicked(b);
    });
    topGrid.add(b, col, 0);
}
```

Bij aanmaak van elk Button object wordt verwezen naar de methode die opgeroepen moet worden als erop geklikt wordt \(`buttonClicked`\).

```java
private void buttonClicked(Button b) {

    int col = Integer.parseInt(b.getText()) - 1;
    connect4Game.doMoveCurrentPlayer(col);

}
```

Ook de kleur van een Circle zal je regelmatig moeten veranderen. Maak hiervoor volgende twee methodes:

```java
private void changeCircleColor(int row, int col, Color c) {
    Circle circle = getCircle(row, col);
    circle.setFill(c);
}

private Circle getCircle(int row, int col) {
    for (Node node : boardGridPane.getChildren()) {
        if (node instanceof Circle) {
            if (node.getId().equals(makeId(col, row))) {
                return (Circle) node;
            }
        }
    }
    return null;
}
```

Op dit moment ziet het klassendiagram van het project er zo uit:

![](/assets/uml3.png)Niet alle methodes staan in deze cursus uitgewerkt, aangezien het belangrijk is zelf te proberen deze te implementeren.

Ik overloop nog even de functionaliteit van de niet uitgewerkte methodes in de GUI klasse.

![](/assets/GUI_UML.png)

Aangezien er een pijl wijst van `Connect4BoardGUI` naar `Connect4Game` weet je dat de `Connect4BoardGUI` klasse een variabele bijhoudt van het type `Connect4Game` zodat deze steeds kan communiceren met de Game klasse.

```java
private Connect4Game connect4Game;
```

Hier maak je best een setter voor, zodat je deze vanuit de Main klasse kan meegeven.

Het aantal rijen of kolommen kan je uit de constraints van `GridPane` afleiden, bvb.

```java
public int getNumberOfRows() {
    return boardGridPane.getRowConstraints().size();
}
```

De methode `getHighestFreeIndex` geeft de rij-index weer van het eerste lege veld.

`isBoardFull` geeft weer of het bord vol zit, `isColumnFull` dan weer of een kolom vol zit.

`legalMoves` geeft een int array weer, met alle legale zetten. Dat zijn de kolommen die niet vol zitten.

### Player

Deze **abstracte klasse** houdt de naam en de kleur van een klasse bij, voorziet hiervoor getters en setters en bevat verder de methode `doMove`. Deze roept dan simpelweg de methode doMove van het `Connect4BoardGUI` object aan.

```java
    public boolean doMove(int col, Connect4BoardGUI connect4BoardGUI) {
        return connect4BoardGUI.doMove(col, color);
    }
```

Het is de bedoeling dat je hiervan twee subklassen maakt, één voor human players en één voor computer players.

### Connect4Game

![](/assets/c4Game_UML.png)

Deze klasse begint als volgt:

```java
public class Connect4Game {
    private Connect4BoardGUI controller;
    private Player player1;
    private Player player2;
    private Player currentPlayer;
```

Ze houdt dus bij welke de controller klasse is. Deze wordt meegegeven in de constructor, alsook de beide `Player` objecten. `currentPlayer` kan je hier dan altijd gelijk zetten aan `player1`.

### Connect4Eval

Deze klasse houdt eigenlijk opnieuw alle gegevens van het bord bij, deze keer in int en int variabelen, wat veel sneller werkt dan GridPane objecten. Hier laat ik jullie zelf de implementatie maken a.d.h.v. het klassendiagram.

Toch enkele startpunten:

In de klasse `Connect4BoardGUI` kan je een `Connect4Eval` object opvragen:

```java
public Connect4Eval getEval() {
    Player player1 = connect4Game.getPlayer1();
    Player player2 = connect4Game.getPlayer2();
    Player current = connect4Game.getCurrentPlayer();

    if (current.getColor() == player1.getColor()) {
        return new Connect4Eval(getBoardIntArray(), color2Int(player1.getColor()), color2Int(player2.getColor()), color2Int(current.getColor()) );
    } else {
        return new Connect4Eval(getBoardIntArray(), color2Int(player1.getColor()), color2Int(player2.getColor()), color2Int(current.getColor()) );
    }
}

public int[][] getBoardIntArray() {
    int[][]board = new int[getNumberOfRows()][getNumberOfColumns()];
    for (int row = 0; row < getNumberOfRows(); row++) {
        for (int col = 0; col < getNumberOfColumns(); col++) {
            Color color = getCircleColor(row, col);
            board[row][col] = color2Int(color);
        }
    }
    return board;
}

public static int color2Int(Color color) {
    if (color == COLOR_YELLOW) {
        return INT_COLOR_YELLOW;
    } else if (color == COLOR_RED) {
        return INT_COLOR_RED;
    } else {
        return INT_COLOR_EMPTY;
    }
}
```

In `Connect4Eval` vind je dan bvb. volgende velden terug.

```java
//het board zal nu in een 2D array bijgehouden worden, ipv een GridPane. De players houden nu een int bij met hun kleur.
private int[][]board;
private int player1;
private int player2;
private int currentPlayer;
```

`gameWon()` roept `gameWon(int color)` aan. Deze kijkt dan weer of er in de arrays van de diagonalen, de rijen of de kolommen een 4-op-een-rij gevonden is.

```java
    public boolean gameWon() {
        boolean player1Won = gameWon(player1);
        boolean player2Won = gameWon(player2);


        return player1Won || player2Won;
    }

    public boolean gameWon(int player) {
        return isWinInRows(player) || isWinInColumns(player) || isWinInDiagonals(player);
    }

    private boolean isWinInDiagonals(int player) {

        int[] d1 = {board[3][0], board[2][1], board[1][2], board[0][3]};
        int[] d2 = {board[4][0], board[3][1], board[2][2], board[1][3], board[0][4]};
        int[] d3 = {board[5][0], board[4][1], board[3][2], board[2][3], board[1][4], board[0][5]};
        int[] d4 = {board[5][1], board[4][2], board[3][3], board[2][4], board[1][5], board[0][6]};
        int[] d5 = {board[5][2], board[4][3], board[3][4], board[2][5], board[1][6]};
        int[] d6 = {board[5][3], board[4][4], board[3][5], board[2][6]};
        int[] d7 = {board[2][0], board[3][1], board[4][2], board[5][3]};
        int[] d8 = {board[1][0], board[2][1], board[3][2], board[4][3], board[5][4]};
        int[] d9 = {board[0][0], board[1][1], board[2][2], board[3][3], board[4][4], board[5][5]};
        int[] d10 = {board[0][1], board[1][2], board[2][3], board[3][4], board[4][5], board[5][6]};
        int[] d11 = {board[0][2], board[1][3], board[2][4], board[3][5], board[4][6]};
        int[] d12 = {board[0][3], board[1][4], board[2][5], board[3][6]};

        return isWinInArray(d1, player)
                || isWinInArray(d2, player)
                || isWinInArray(d3, player)
                || isWinInArray(d4, player)
                || isWinInArray(d5, player)
                || isWinInArray(d6, player)
                || isWinInArray(d7, player)
                || isWinInArray(d8, player)
                || isWinInArray(d9, player)
                || isWinInArray(d10, player)
                || isWinInArray(d11, player)
                || isWinInArray(d12, player);
    }

    private boolean isWinInRows(int player) {
        for (int row = 0; row < getNumberOfRows(); row++) {
            if(isWinInArray(board[row], player)) {
                return true;
            }
        }
        return false;
    }

    private boolean isWinInColumns(int player) {
        for (int col = 0; col < getNumberOfColumns(); col++) {

            if(isWinInArray(getCol(col), player)) {
                return true;
            }
        }
        return false;
    }

    private int[] getCol(int col) {
        int[] array = new int[getNumberOfRows()];
        for (int r = 0; r < array.length; r++) {
            array[r] = board[r][col];
        }
        return array;
    }
```



