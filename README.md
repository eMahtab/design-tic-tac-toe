# Design Tic Tac Toe
## https://leetcode.com/problems/design-tic-tac-toe

Assume the following rules are for the tic-tac-toe game on an n x n board between two players:

1. A move is guaranteed to be valid and is placed on an empty block.
2. Once a winning condition is reached, no more moves are allowed.
3. A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.

```
Implement the TicTacToe class:

TicTacToe(int n) Initializes the object the size of the board n.

int move(int row, int col, int player) Indicates that the player with id player plays at the cell (row, col) of the board.
The move is guaranteed to be a valid move.
```
# Implementation 1 : Check the row, check column, check main diagonal, check opposite diagonal
The `player` can only win when he makes the move. Because player 1 will only make 1 and player 2 will only make 2. 
So player 1 will never mark a 2 on the tic-tac-toe board and similalry player 2 will never mark a 1 on the board.

```java
class TicTacToe {
    int[][] board;
    public TicTacToe(int n) {
        board = new int[n][n];
    }
    
    public int move(int row, int col, int player) {
        board[row][col] = player;
        int win = checkBoard(row,col,player);
        return win;
    }
    
    private int checkBoard(int row, int col, int player) {
        //check the row
        int rowCount = 0;
        for(int j = 0; j < board[0].length; j++) {
            if(board[row][j] != player)
                break;
            else
                rowCount++;
        }
        if(rowCount == board.length)
            return player;
        
        //check the column
        int colCount = 0;
        for(int i = 0; i < board.length; i++) {
            if(board[i][col] != player)
                break;
            else
                colCount++;
        }
        if(colCount == board.length)
            return player;
        
        //check the main diagonal
        int mainDiagonalCount = 0;
        for(int i = 0; i < board.length; i++) {
            if(board[i][i] != player)
                break;
            else
               mainDiagonalCount++; 
        }
        if(mainDiagonalCount == board.length)
            return player;
        
        //check opposite diagonal
        int oppositeDiagonalCount = 0;
        int n = board.length;
        for(int i = 0; i < board.length; i++) {
            if(board[i][n-1-i] != player)
                break;
            else
               oppositeDiagonalCount++; 
        }
        if(oppositeDiagonalCount == board.length)
            return player;
        
        return 0;
    }
}
```

# Implementation 2 : Refactoring of implementation 1
```java
class TicTacToe {
    int[][] board;
    public TicTacToe(int n) {
        board = new int[n][n];
    }
    
    public int move(int row, int col, int player) {
        board[row][col] = player;
        
        if(checkRow(row,player) || checkColumn(col,player) ||
           checkMainDiagonal(player) || checkOppositeDiagonal(player))
            return player;
        
        return 0;
    }
        
    private boolean checkRow(int row, int player) {
        for(int j = 0; j < board[0].length; j++) {
            if(board[row][j] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkColumn(int col, int player) {
        for(int i = 0; i < board.length; i++) {
            if(board[i][col] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkMainDiagonal(int player) {
        for(int i = 0; i < board.length; i++) {
            if(board[i][i] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkOppositeDiagonal(int player) {
        int n = board.length;
        for(int i = 0; i < board.length; i++) {
            if(board[i][n-1-i] != player)
                return false;
        }
        return true;
    }
}

```

# Implementation 3 : Check Main and Opposite diagonals based on player move(row,col)

We should only check main diagonal if the move was made on main diagonal, for any cell on main diagonal `row == col`

Similarly we should only check opposite diagonal if the move was made on opposite diagonal, for any cell on opposite diagonal `row+col == board.length - 1`

![Tic Tac Toe](example.JPG?raw=true)

```java
class TicTacToe {
    int[][] board;
    public TicTacToe(int n) {
        board = new int[n][n];
    }
    
    public int move(int row, int col, int player) {
        board[row][col] = player;
        
        if(checkRow(row,player) || checkColumn(col,player) ||
           // we should only check main diagonal if the move was made on main diagonal
           (row == col && checkMainDiagonal(player)) || 
           // we should only check opposite diagonal if the move was made on opposite diagonal
           ((row+col == board.length-1) && checkOppositeDiagonal(player)) )
            return player;
        
        return 0;
    }
        
    private boolean checkRow(int row, int player) {
        for(int j = 0; j < board[0].length; j++) {
            if(board[row][j] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkColumn(int col, int player) {
        for(int i = 0; i < board.length; i++) {
            if(board[i][col] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkMainDiagonal(int player) {
        for(int i = 0; i < board.length; i++) {
            if(board[i][i] != player)
                return false;
        }
        return true;
    }
    
    private boolean checkOppositeDiagonal(int player) {
        int n = board.length;
        for(int i = 0; i < board.length; i++) {
            if(board[i][n-1-i] != player)
                return false;
        }
        return true;
    }
}

```

# References :
1. https://leetcode.com/problems/design-tic-tac-toe/solution
2. https://leetcode.com/problems/design-tic-tac-toe/discuss/163279/Java-naive-o(4n)-solution-by-checking-row-col-and-two-diagonals-each-time
