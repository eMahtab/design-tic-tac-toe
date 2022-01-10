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

# Implementation :
```java
class TicTacToe {
    int[][]board;
    
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        board = new int[n][n];
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        this.board[row][col] = player;
        
        if(checkRow(row,player) || checkColumn(col, player))
            return player;
        
        if(row == col && checkLeftDiagonal(player))
            return player;
        
        if(row + col == board.length - 1 && checkRightDiagonal(player))
            return player;
        
        return 0;
    }
    
    private boolean checkRow(int row, int player) {
        for(int col = 0;  col < board[0].length; col++) {
            if(board[row][col] != player)
                return false;
        }
        return true;
    }
    private boolean checkColumn(int col, int player) {
        for(int row = 0; row < board.length; row++) {
            if(board[row][col] != player)
                return false;
        }
        return true;
    }
    private boolean checkLeftDiagonal(int player) {
        for(int row = 0; row < board.length; row++) {
            if(board[row][row] != player)
                return false;
        }
        return true;
    }
    private boolean checkRightDiagonal(int player) {
        for(int row = 0; row < board.length; row++) {
            if(board[row][board.length - 1 - row] != player)
                return false;
        }
        return true;
    }
}
```

# References :
https://leetcode.com/problems/design-tic-tac-toe/discuss/163279/Java-naive-o(4n)-solution-by-checking-row-col-and-two-diagonals-each-time
