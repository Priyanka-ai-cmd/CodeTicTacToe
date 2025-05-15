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













