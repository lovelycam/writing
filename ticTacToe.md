## Tic-Tac-Toe
An enjoyable and strategic two-player game!

#### Overview
Assign one player the letter `X` and the other player `O`. Players take turns drawing their letters on a simple grid. The first player to draw three letters in a row wins.

#### Setup
Draw a game board grid that is 3 squares by 3 squares.
 
#### Gameplay
A heads-or-tails coin toss determines who goes first. The winner draws their letter in any square on the game board grid. The other player then draws their letter in any open square. 

Players alternate drawing their letters in open squares until there are three of the same letter in a row (horizontal, vertical, or diagonal). This is considered a win. The winner of the game goes first in the next round.

A game results in a stalemate if all 9 squares are filled before a player wins.

#### Strategy
Generally the first player dominates because they can draw their letter in any square. Drawing in corner squares is advantageous, as it sets up three possible directions to win: horizontal, vertical, and diagonal. 

The second player must decide if they will draw defensively, e.g. should they block the first player from drawing three in a row. Forcing a stalemate is often an appropriate defensive strategy since this will force a coin toss, and will allow for the possibility to go first and control the next game.
