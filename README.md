# Design Tic Tac Toe

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

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
```
