//Here we are going to implement makeMove() and undo() function
//In Game class, inside makeMove() method 

public class Game{

        public void makeMove(){
        Player currentPlayer = players.get(nextPlayerIndex);
        System.out.println("It's" + currentPlayer.getName() + "'s turn. Please make a move");
        currentPlayer.makeMove();
    }
}
//Here you are asking the Player to make a move
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now go to the Player class and create a makeMove function over here
//Now for HUMAN and BOT, will the makeMove() method be same or different

public class Player{

    public abstract makeMove(Board board);

//In both the classes we will implement makeMove()

public class HumanPlayer extends Player{

    public Move makeMove(Board board){
    }
 // To make the move do we need the board   
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Inside HumanPlayer class -> get the row and col through scanner input from the user

public class HumanPlayer extends Player{

    private Scanner scanner = new Scanner(System.in);

    public Move makeMove(Board board){
    
        System.out.println("Please enter the row in which you want to place the symbol");
        int r = scanner.nextInt();
        System.out.println("Please enter the col in which you want to place the symbol");
        int c = scanner.nextInt();

        return new Move(new Cell(r, c), this);
    
    }
}

//since we have row & col now, so we can generate move out of this particular thing
//move needs 2 particular thing -> Cell and Player(as per argument in Move class)
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Player has made a move now we should be updating the actual cell int board
//and before that we should validate the move
//as well as check whether the cell is not occupied

public class Game{

      public boolean validateMove(Move move){
          int r = move.getCell().getRow();
          int c = move.getCell().getRow();

          if(r < 0  || c < 0 || r > board.getGrid().size() -1 || c > board.getGrid().size()){
              return false;
          }
          if(board.getGrid().get(r).get(c).getCellState().equals(CellState.FILLED)){
              return false;
          }
          return true;
      }    
      
      
      public void makeMove(){
          Player currentPlayer = players.get(nextPlayerIndex);
          System.out.println("It's" + currentPlayer.getName() + "'s turn. Please make a move");
          Move move = currentPlayer.makeMove(board);
    }

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//now in the makeMove() method, write if validation checks fails, throw exception 

public class game{

    public void makeMove(){
        Player currentPlayer = players.get(nextPlayerIndex);
        System.out.println("It's" + currentPlayer.getName() + "'s turn. Please make a move");
        Move move = currentPlayer.makeMove(board);
        
        if(!validateMove(move)){
            throw new RuntimeException("Invalid move! Please try again");
        }
    }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//this exception will be handled by gameController
//put a try catch inside makeMove()

public class GameController{
    public void makeMove(Game game){
        try{
            game.makeMove();
        }catch(Exception e){
            System.out.println(e.getMessage());
        }
    }
    
// in the Controller, we are catching the exception
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Now next is to update the board and nextPlayerIndex

public class Game{

    public void makeMove(){
        Player currentPlayer = players.get(nextPlayerIndex);
        System.out.println("It's" + currentPlayer.getName() + "'s turn. Please make a move");
        Move move = currentPlayer.makeMove(board);
         
        if(!validateMove(move)){
            throw new RuntimeException("Invalid move! Please try again");
        }
        
        int row = move.getCell().getRow();
        int col = move.getCell().getCol();
        
        Cell cell = board.getGrid().get(row).get(col);
        cell.setCellState(CellState.FILLED);
        cell.setSymbol(currentPlayer.getSymbol());
    
        nextPlayerIndex +=1;
        nextPlayerIndex %= players.size();

        move.setCell(cell);
        moves.add(move);
        
    }

//updating the nextPlayerIndex -> incrementing -> nextPlayerIndex +=1;
//your nextPlayerIndex should come back at 0th index when all the person's turn get over -> so we need to take mod -> nextPlayerIndex %= player.size();
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//now whatever move we have created we have to add that move into the list of move also -> move.setCell(cell);
//but before that update the move with actual cell
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//after every move we need to update the state of the game by checking if winner is there or not

public class Game{

        public boolean checWinner(){
        public void makeMove{
                //update the state of the game
                
                if(checkWinner(move)){
                    setWinner(currentPlayer);
                    setGameState(GameState.SUCCESS);
                } else if(moves.size() == board.getSize() * board.getSize()){
                    setWinner(null);
                    setGameState(GameState.DRAW);
            
                }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//one by one we need to check all the strategies which are there, and if any strategy gives true, that means you have a winner

public class Game{

    public boolean checkWinner(Move move){
        for(WinningStrategy winningStrategy : winningStrategies){
            if(winningStrategy.checkWinner(board, move)){
                return true;
            }
        }
        return false;
    }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//lets add strategy inside client
public class Client {

    public static void main(String[] args) {
        GameController gameController = new GameController();
        
        List<WinningStrategy> winningStrategies = new ArrayList<>();
        winningStrategies.add(new RowWinningStrategy());
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

//define makeMove inside BotPlayer since one of the player is bot

public class BotPlayer extends Player{
    private BotDifficultyLevel botDifficultyLevel;
    private BotPlayingStrategy botPlayingStrategy;

    @Override
    public Move makeMove(Board board){
        return botPlayingStrategy.makeMove(board, this );
    }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//changing 'void return type'inside EasyBotPlayingStrategy to Move

public class EasyBotPlayingStrategy implements BotPlayingStrategy{

    @Override
    public void makeMove(Board board, Player player) {
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
// and changing 'void' inside interface BotPlayingStrategy to Move


    public interface BotPlayingStrategy {
    Move makeMove(Board board, Player player);
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Creating Exceptions package coz something happened and our exception was not been captured

public class InvalidMoveException extends Exception{
    public InvalidMoveException(String message){
        super(message);
    }
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Appying this in Game class

   public void makeMove() throws InvalidMoveException{
         
        if(!validateMove(move)){
            throw new InvalidMoveException("Invalid move! Please try again!");
        }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

// now in gameController

public class gameController

    public void makeMove(Game game){
        try{
            game.makeMove();
        }catch(InvalidMoveException e){
            System.out.println(e.getMessage());
        }catch (Exception e){
            System.out.println(e.getStackTrace());
        }
    }
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//Implementing Undo() method

//Under Client()

public class Client{
        private static Scanner scanner = new Scanner(System.in);
        public static void main(String[] args){
        
                while(gameController.checkState(game).equals(GameState.IN_PROGRESS)){
                    gameController.makeMove(game);
                    gameController.display(game);
            
                    System.out.println("Do you want to Undo [Y/N]");
                    String undoResponse = scanner.nextLine();
                    if(undoResponse.equals("Y")){
                        gameController.undo(game);
                        System.out.println("Undo is successful");
                        gameController.display(game);
                    }        
            
                }
------------------------------------------------------------------------------------------------------------------------------------
//Under GameController()        

public void undo(Game game){
        game.undo();
}

------------------------------------------------------------------------------------------------------------------------------------

//since there is no undo function in the game, so lets go and define undo
public class Game{

        public void undo(){
        if(moves.isEmpty()){
            System.out.println("No moves present. Can't Undo");
            return;
        }
        Move lastMove = moves.get(moves.size()-1);
        moves.remove(moves.size()-1);
        
        Cell cell = lastMove.getCell();
        cell.setCellState(CellState.EMPTY);     //Setting last cellState to be EMPTY
        cell.setSymbol(null);
        
//        nextPlayerIndex -=1;
//        (a -b) % n = (a - b + n) % n
        nextPlayerIndex = (nextPlayerIndex -1 + players.size()) % players.size();
    }
    
------------------------------------------------------------------------------------------------------------------------------------

//We need to handle Undo by removing cell (undo) values from HashMap -> decrease the frequency of teh HashMap

public WinningStrategy{

    void handleUndo(Board board, Move move); 
}
------------------------------------------------------------------------------------------------------------------------------------

public RowWinningStrategy{

@Override
    public void handleUndo(Board board, Move move){
        int row = move.getCell().getRow();
        Symbol symbol = move.getPlayer().getSymbol();
        
        rowCount.get(row).put(symbol.getCharSymbol(), rowCount.get(row).get(symbol.getCharSymbol()) -1 );
    }

------------------------------------------------------------------------------------------------------------------------------------

public class Game{

   public void makeMove() throws InvalidMoveException{
        
//        nextPlayerIndex -=1;
//        (a -b) % n = (a - b + n) % n
        nextPlayerIndex = (nextPlayerIndex -1 + players.size()) % players.size();
        
        for(WinningStrategy winningStrategy : winningStrategies){
            winningStrategy.handleUndo(board, lastMove);
        }
    }
------------------------------------------------------------------------------------------------------------------------------------
//Now we need to update the state of the game

public class Game{
    public void undo(){
        
        for(WinningStrategy winningStrategy : winningStrategies){
            winningStrategy.handleUndo(board, lastMove);
        }
        
        setWinner(null);
        setGameState(GameState.IN_PROGRESS);
    }
    
  
