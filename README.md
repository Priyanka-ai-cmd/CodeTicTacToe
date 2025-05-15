# CodeTicTacToe
public class Game{

    private Board board;
	
    private List<Player> players;
    private Player winner;
    private int nextPlayerIndex;
    private List<Move> moves;
    private GameState gameState;
    private List<WinningStrategy> winningStrategies;

}

public class Board{

    private int size;
    private List<List<Cell>> grid;
}

public abstract class Player{

    private int id;
    private PlayerType playerType;
    private String name;
    private Symbol symbol;

}

public class BotPlayer extends Player{

    private BotDifficultyLevel botDifficultyLevel;
}

public class HumanPlayer extends Player{    
}

public class Move{
    private Cell cell;
    private Player player;
}

public class Cell {
    private int row;
    private int col;
    private CellState cellState;
    private Symbol symbol;
}

public enum BotDifficultyLevel {
    EASY,
    MEDIUM,
    HARD
    
}
public enum CellState {
    EMPTY,
    FILLED
}

public enum GameState {
    IN_PROGRESS,
    DRAW,
    SUCCESS 
}

public enum PlayerType {
     HUMAN,
     BOT    
}
public class Symbol {
    private char charSymbol;
    private String color;
}

//Now come to the Client, so Client will be interacting with GameController so we need a GameController object.
public class Client {
    public static void main(String[] args) {
        GameController gameController = new GameController;
    }
}

//Now when we create an object of Gamcontroller inside the client, now when we want to start the game, we will ask gamecontroller, hey gamecontroller can you start the game
//So controller will definitely have a method called start game

public class GameController {
    public void startGame(){
        
    }
}
//Now after start game, it should display also -> so lets have a method called display.
//Now the client will also ask to make a move -> lets have a method makeMove.
//Again client may ask to check the state also -> checkState and so on

public class GameController {
    public void startGame(){
        
    }
    public void display(){
        
    }
    public void makeMove(){
        
    }
    public void checkState(){
        
    }
    public void undo(){
        
    }
    public Player getWinner(){
        return null;
    }

}

//These are the methods, client might be asking to start the game. To start the game, controller might be creating a game object 
//Then you go to the client, and command GameController to start the game 

public class Client {
    public static void main(String[] args) {
        GameController gameController = new GameController();        
        gameController.startGame();
    }
}
//When you start a game, game controller would already created a game inside and you can play the game
//You can first of all display the initial state
//Then when you play the game -> while(gameController.checkStatus().equals -> IN PROGRESS) 
//Right now checkStatus is not returning anything so we change the return type from void to game.
// So go to the GameController 
public class GameController {
    private Game game;
    
    public void startGame(){
        this.game = new Game();
    }
    public void display(){
        
    }
    public void makeMove(){
        
    }
    public GameState checkState(){
        return GameState.IN_PROGRESS;
    }
    public void undo(){
        
    }
    public Player getWinner(){
        return null;
    }

}
//Now go to the CLient -> while(gameController.checkState().equals(GameState.IN_PROGRESS)) -> if gamestate is in progress -> keep playing the game
public class Client {
    public static void main(String[] args) {
        GameController gameController = new GameController();
        gameController.startGame();
        gameController.display();
        while(gameController.checkState().equals(GameState.IN_PROGRESS)){
            gameController.makeMove();
            gameController.display();   
        }
    }
}

//Now we were playing the game, and if the state chnage to something else, while loop will end, means the game is ended
//Here when the game ends, first we will check there is a winner or not. 
public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();
        
        gameController.startGame();
        gameController.display();
        while(gameController.checkState().equals(GameState.IN_PROGRESS)){
            gameController.makeMove();
            gameController.display();
            
        }
        if(gameController.checkState().equals(GameState.SUCCESS)){
            System.out.println("Winner is" + gameController.getWinner());
        }else if(gameController.checkState().equals(GameState.DRAW)){
            System.out.println("Game ends in a DRAW!");
        }
    }
}
//Now there is one issue in this. If one game is going on. and I have to play one more game then what I have to do
//If I have to tart one more game simultaneously, I have to create a new object of game controller but every game should not be starting a new game controller
//we are supposed to have only one object of game controller

  public class GameController {
    //private Game game;
    
    public Game startGame(){
        return new Game(); 
    }
 }


public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();       
        Game game = gameController.startGame();
    }
}

//Now once the game is defined, in other methods like display or checkStatus -> you have to tell which game you want to display

public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();
        
        Game game = gameController.startGame();
        
        gameController.display(game);
        while(gameController.checkState(game).equals(GameState.IN_PROGRESS)){
            gameController.makeMove(game);
            gameController.display(game);
            
        }
        if(gameController.checkState(game).equals(GameState.SUCCESS)){
            System.out.println("Winner is" + gameController.getWinner(game));
        }else if(gameController.checkState(game).equals(GameState.DRAW)){
            System.out.println("Game ends in a DRAW!");
        }
    }
}
 
//Now modify all the return types of methods in gameController

public class GameController {
    public Game startGame(){
        return new Game(); 
    }
    public void display(Game game){
    }
    public void makeMove(Game game){
    }
    public GameState checkState(Game game){
        return GameState.IN_PROGRESS;
    }
    public void undo(Game game){
    }
    public Player getWinner(Game game){
        return null;
    }
}

// Now uptill now we have created a Game flow
//Now lets come to the Game class and from this what all attributes I require at the start of the game, i want 3 things from the client -> 
//the board size, list of players who are playing & what are the winningStrategies you want & difficultyLevel of bot if there is a bot
//So in GameController, we will add those attributes which we are expecting at the start of the game.

public class GameController {
    //private Game game;
    
    public Game startGame(int dimension, List<Player> players,List<WinningStrategy> winningStrategies){
        return new Game();
    }
-----------------------------------------------------------------------------------------
//Now we to the client

//We will go and create constructor in player since we have not created.
//For every model, make sure you create constructor for each class
--------------------------------------------------------------------------------------------
  public class Client {

    public static void main(String[] args) {
            GameController gameController = new GameController();

            List<Player> players = new ArrayList<>();
            players.add(new Player());
..........................................................................................................
public abstract class Player {
    private int id;
    private PlayerType playerType;
    private String name;
    private Symbol symbol;

    public Player(int id, PlayerType playerType, String name, Symbol symbol){
        this.id = id;
        this.playerType = playerType;
        this.name = name;
        this.symbol = symbol;
    }    

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();

        List<Player> players = new ArrayList<>();
        players.add(new HumanPlayer(1, PlayerType HUMAN, "Mohit", 'x'));

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Here we donot have constructor in HumanPlayer -> giving a red underline -> we will create a constructor
//Since we donot have constructor, it is giving an error
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
public class HumanPlayer extends Player{
    public HumanPlayer(int id, PlayerType playerType, String name, Symbol symbol){
        
    }
}
........................................................................................................................
//Here inside the constructor, we cannot write this.id = id, this.playertype = playertype and so on
//Since these attributes are private (declared inside Player class) we cannot access here inside HumanPlayer

public abstract class Player {
    private int id;
    private PlayerType playerType;
    private String name;
    private Symbol symbol;
 ........................................................................................................................
//so we will use super keyword.
//so HumanPlayer will call this super constructor

public class HumanPlayer extends Player{
    public HumanPlayer(int id, PlayerType playerType, String name, Symbol symbol){
       super(id, playerType, name, symbol); 
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
public class Client {
    public static void main(String[] args) {
        GameController gameController = new GameController();

        List<Player> players = new ArrayList<>();
        players.add(new HumanPlayer(1, PlayerType.HUMAN, "Priyanka", new Symbol('x', "Green"))) ;

...........................................................................................................
//Now add one more player -> BOT
public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();

        List<Player> players = new ArrayList<>();
        players.add(new HumanPlayer(1, PlayerType.HUMAN, "Priyanka", new Symbol('x', "Green"))) ;
        players.add(new HumanPlayer(1, PlayerType.HUMAN, "Priyanka", new Symbol('x', "Green"))) ;

------------------------------------------------------------------------------------------------------------------------
//Now modify BotPlayer class

public class BotPlayer extends Player{
    private BotDifficultyLevel botDifficultyLevel;

    public BotPlayer(int id, PlayerType playerType, String name, Symbol symbol, BotDifficultyLevel botDifficultyLevel){
        super(id, playerType, name, symbol);
        this.botDifficultyLevel = botDifficultyLevel;
    }
**-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**
//Add botPlayer to the Client

public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();

        List<Player> players = new ArrayList<>();
        players.add(new HumanPlayer(1, PlayerType.HUMAN, "Priyanka", new Symbol('x', "Green"))) ;
        players.add(new BotPlayer(2, PlayerType.BOT, "Bot 1", new Symbol('o', "Blue"), BotDifficultyLevel.EASY));

**-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**
//Now in teh startGame method, we have 3 attributes -> dimension, players & winningStrategies. 
//We will supply those arguments in the clients startGame
//Before that we will create List of WinningStrategy

public class Client {
    public static void main(String[] args) {
        GameController gameController = new GameController();

        List<Player> players = new ArrayList<>();
        players.add(new HumanPlayer(1, PlayerType.HUMAN, "Priyanka", new Symbol('x', "Green"))) ;
        players.add(new BotPlayer(2, PlayerType.BOT, "Bot 1", new Symbol('o', "Blue"), BotDifficultyLevel.EASY));
        
        List<WinningStrategy> winningStrategies = new ArrayList<>();
        
        Game game = gameController.startGame(3, players, winningStrategies);

**-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------**
//Now we are going to design a Builder design Pattern inside Game class
//For Builder Design Pattern we need a static nested class
//In builder, we donot want to create all attribute, only those attributes which we need for creation of object -> supply to client
.........................................................................................................................................
public class Game {
    public static class Builder{
        private int dimension;
        private List<Player> players;
        private List<WinningStrategy> winningStrategies;

        public Builder setDimension(int dimension) {
            this.dimension = dimension;
            return this; 
        }

        public Builder setPlayers(List<Player> players) {
            this.players = players;
            return this;
        }

        public Builder setWinningStrategies(List<WinningStrategy> winningStrategies) {
            this.winningStrategies = winningStrategies;
            return this;
        }

        //In this we need to have a build method
        public Game build(){
            return new Game();
        }
      **-------------------------------------------------------------------------------------------------------------------------------------------------------------------------**
//Also in the Game we need to hav a method -> Get Builder
//Make the getBuilder method static

public class Game{
    public static Builder getBuilder(){
        return new Builder();
    }
    public static class Builder{
        private int dimension;
        private List<Player> players;
        private List<WinningStrategy> winningStrategies;
.....................................................................................................................................................................
//create a Game constructor
private Game(){
        
}
--------------------------------------------------------------------------------------------------------------------
// Here in GameController under startGame
public class GameController {
    //private Game game;
    
    public Game startGame(int dimension, List<Player> players,List<WinningStrategy> winningStrategies){
        return Game
                .getBuilder()
                .setDimension(dimension)
                .setPlayers(players)
                .setWinningStrategies(winningStrategies)
                .build();
    }
//with this your game will be build.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//You can also add single single player instead of adding a list
//lets say tomorrow you want to add a new player, you can add a new player

public class Game {
   public static class Builder{
          private int dimension;
          private List<Player> players;
          private List<WinningStrategy> winningStrategies;
  
          public Builder addPlayer(Player player){
              this.players.add(player);
              return this;
          }
  
//and in Game Controller

public class GameController {    
    public Game startGame(int dimension, List<Player> players,List<WinningStrategy> winningStrategies){
        return Game
                .getBuilder()
                .setDimension(dimension)
                .addPlayers(players.get(0))
                .addPlayers(players.get(1)) 
                .setWinningStrategies(winningStrategies)
                .build();

//This is another option
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//We created Builder for validation purpose
//If you remember there are 3 validations -> 
//1. At max 1 Bot in the game
//2. Players size= dimension -1
//3. Every player should have separate symbol

public class Game {
   public static class Builder{
        public void validate(){
            if(players.size() != dimension-1){
                throw new RuntimeException("Invalid players count");
            }
        }
...............................................................................................................................................................
//Once the validation happens, you will pass the builder object over here -> return new Game(this)
//Pass builder in the constructor
public class Game {

    private Game(Builder builder){
        this.board = new Board();
        this.players = builder.players;
        this.winningStrategies = builder.winningStrategies;
        this.winner = null;
        this.nextPlayerIndex = 0;
        this.moves = new ArrayList<>();
        this.gameState = GameState.IN_PROGRESS;
    }
   public static class Builder{
        public Game build(){
            validate();
            return new Game(this);
        }
//SO over here when Game will be called, a new board will be created -> this.board = new Board();
//So passing the dimension inside the board
    private Game(Builder builder){
        this.board = new Board(builder.dimension);
        this.players = builder.players;
        this.winningStrategies = builder.winningStrategies;
        this.winner = null;
        this.nextPlayerIndex = 0;
        this.moves = new ArrayList<>();
        this.gameState = GameState.IN_PROGRESS;
-------------------------------------------------------------------------------------------------------------------------------------------
//Accordingly in the board class -> lets create a board
//We have to create a n * n board
//First lets create an empty grid and we will keep adding that much #of cells which is required

public class Board {
    private int size;
    private List<List<Cell>> grid;

    public Board(int size){
         this.size = size;
         this.grid = new ArrayList<>();
         for(int i =0; i<size; i++){
             grid.add(new ArrayList<>());   //Create a new row
             for(int j =0; j <size; j++){
                 grid.get(i).add(new Cell()); // and for each row, creating a cell
             }
         }
    }

  //so this grid s a 2D array -> so we are created the outer list and then for every row we are adding a new list.
  // in that list we are going and adding that much amount of cells as many required
-------------------------------------------------------------------------------------------------------------------------------------------------------
//Now in cell we might need certain things so lets create a constructor of cell also in cell class.

public class Cell {
    public Cell(int row, int col){
        this.row = row;
        this.col = col;
        this.cellState = CellState.EMPTY; //till when the cell is constructed, we will keep this empty
        this.symbol = null;
    }
  
..........................................................................................................
//Now go to the board

public class Board {
    public Board(int size){
         this.size = size;
         this.grid = new ArrayList<>();
         for(int i =0; i<size; i++){
             grid.add(new ArrayList<>());   
             for(int j =0; j <size; j++){
                 grid.get(i).add(new Cell(i, j)); 
             }
         }
    }

//and type -> new Cell(i, j) for now
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now lets create a constructor for classes which donot have a constructor
public class Move {
    private Cell cell;
    private Player player;

    public Move(Cell cell, Player player){
        this.cell = cell;
        this.player = player;
    }
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  //startGame is done, now we want to display
  //Lets have a method in game for display
public class Game{
      public void display(){
        
    }
}
.............................................................................................................................................
//So from the GameController, we are saying hey GameCOntroller, display your details

public class GameController{
    public void display(Game game){
        game.display();
    }

.....................................................................................................................................................
//Now coming back to game, you want to display board
//So game will ask board class to display yourself

public class Game{
    public void display(){
        board.displayBoard();

    }
........................................................................................................................................................
//Now got to board and add a method display

public class Board{
    public void displayBoard(){
    
    }
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now in cell class, we will add a display method in which we will have a clear message of the symbol played
public class Cell{    
    public void display(){
        if(symbol == null){
            System.out.print("| - |");
        } else{
            System.out.print("| - " + symbol.getCharSymbol() + " |");
        }
    }

//So here what happens is GameController -> asks Game to display the board
//Game says its not me who will displat -> its the board -> calls boarddisplay() method
//board -> goes to celldisplay() method
//Now tomorrow if you want to change the way board displays itself -> you will only change the dispaly method inside board
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//So uptil now startGame and display is ready
//Now we have to do checkState and makeMove
//For checkState, I need to go checkState and return getGameState

public class GameController{
    public GameState checkState(Game game){
        return game.getGameState();
    }
    
//Here we have implemented GameState()
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now implementing Winner

public class GameController{    
    public Player getWinner(Game game){
        return game.getWinner();
    }
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//makeMove method and undo() method will be implemented in the next class
//Now designing a strategy by which BotDifficultyLevel -> is made EASY -> we will use Factory Pattern

public class BotPlayingStrategyFactory {
    public static BotPlayingStrategy getBotPlayingStrategy(BotDifficultyLevel botDifficultyLevel){
        if(botDifficultyLevel.equals(BotDifficultyLevel.EASY)){
            return new EasyBotPlayingStrategy();
        }
        return null;
    }
}

//Here we have created a Factory and on the basis of difficulty level you will be using BotPlayingStrategy -> EASY, MEDIUM or HARD
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//You will be doing in BotPlayer. 
//You have already created BotDifficultyLevel object
//create BotPlayingStrategy object also here

public class BotPlayer extends Player{
    private BotDifficultyLevel botDifficultyLevel;
    private BotPlayingStrategy botPlayingStrategy;

    public BotPlayer(int id, PlayerType playerType, String name, Symbol symbol, BotDifficultyLevel botDifficultyLevel){
        super(id, playerType, name, symbol);
        this.botDifficultyLevel = botDifficultyLevel;
        this.botPlayingStrategy = BotPlayingStrategyFactory.getBotPlayingStrategy(botDifficultyLevel);
    }

  //Now your BotPlayingStrategy is ready
  //Whenever you want to make Move -> you will call the makeMove method of EasyBotPlayingStrategy
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now we will be ready our makeMove in EasyBotPlayingStrategy
//For very easy strategy we can put the symbol in the first empty place

public class EasyBotPlayingStrategy implements BotPlayingStrategy{

    @Override
    public void makeMove(Board board, Player player) {
        //put the symbol in the first empty place
        //  int dimension = board.getSize();    
        for(List<Cell> row: board.getGrid()){       //you go to each and every cell and check if teh cell is empty
            for(Cell cell: row){
                if(cell.getCellState().equals(CellState.EMPTY)){
                    cell.setCellState(CellState.FILLED);
                    cell.setSymbol(player.getSymbol());     // so a move has happend
                }
            }
        }
    }
    
}
// So we have implemented a basic WinningStrategy
....................................................................................................................................
//modifying BotPlayingStrategy Interface

public interface BotPlayingStrategy {
    void makeMove(Board board, Player player);
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now coming to RowWinningStrategy
//Under WinningStrategy, we will modify the method -> checkWinner

public interface WinningStrategy {
    public void checkWinner(Board board, Move move){
        
    }
}
//Since we want to tell who made the move() and where the move happened(board)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now lets come implement the checkWinner method over here in RowWinningStrategy()
//For every row, for every symbol - we need to store the count of that -> a winning strategy if whole row is filled, with same symbol -> player has won

// 0: 'x' -> 1
// 0: 'o' -> 1

// 1: 'x' -> 1
// 1: 'o' -> 1

// 2: 'x' -> 1
// 2: 'o' -> 1
//What kind of data staructure I can use? a HashMap
For every row, we will have a hashmap
public class RowWinningStrategy implements WinningStrategy{
    HashMap<Integer, HashMap<Character, Integer>> rowCount = new HashMap<>(); 
    @Override
    public boolean checkWinner(Board board, Move move){
        //for the corresponding move which can be in a row or col -> lets get tha data
        int row = move.getCell().getRow();
        Symbol symbol = move.getCell().getSymbol();
        //first check that if we have any value already stored for that row or not
        if(!rowCount.containsKey(row)){
            rowCount.put(row, new HashMap<>()); //if Map doesnot have nay info about the row in which the move happens, put that key value in Map
        }
        HashMap<Character, Integer> counts = rowCount.get(row); //if yes, lets get that row
        
        if(!counts.containsKey(symbol.getCharSymbol())){        //check if this char is present in the map or not
            counts.put(symbol.getCharSymbol(), 0);
        }
        //increase symbol frequency
        counts.put(symbol.getCharSymbol(), counts.get(symbol.getCharSymbol())+1);
        //if the frequency gets equal to the dimension size, then the winner is there
        if(counts.get(symbol.getCharSymbol()) == board.getSize()) {
            return true;
        }
        return false;
    }
}
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
//
public class GameController{
      public void makeMove(Game game){
        game.makeMove();
    }
....................................

public class Game{
    public void makeMove(){
        
    }


