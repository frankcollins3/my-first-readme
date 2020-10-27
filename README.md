# my-first-readme

```javascript
const handleWin = (letter) => {
    gameIsLive = false;
    if (letter === "x") {
        statusDiv.innerHTML = '${letterToSymbol(letter)} has won!';
    } else {
        statusDiv.innerHTML = '<span>${letterToSymbol(letter)} has won! </span>'
    }
    };
    ```

'``javascript
.grid {
    background-color: salmon;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);git 
    gap: 15px;
    margin-top: 50px;
}
```

```javascript
const player = "O";
const computer = "X";

let board_full = false;
let play_board = ["", "", "", "", "", "", "", "", ""];

const board_container = document.querySelector(".play-area");
| const player and const computer, combined with let boad_full and let play_board are variables I declare to initialize the game.
```

```javascript
check_board_complete = () => {
  let flag = true;
  play_board.forEach(element => {
    if (element != player && element != computer) {
      flag = false;
    }
  });
  board_full = flag;
};


const check_line = (a, b, c) => {
  return (
    play_board[a] == play_board[b] &&
    play_board[b] == play_board[c] &&
    (play_board[a] == player || play_board[a] == computer)
  );
};

const check_match = () => {
  for (i = 0; i < 9; i += 3) {
    if (check_line(i, i + 1, i + 2)) {
      document.querySelector(`#block_${i}`).classList.add("win");
      document.querySelector(`#block_${i + 1}`).classList.add("win");
      document.querySelector(`#block_${i + 2}`).classList.add("win");
      return play_board[i];
    }
  }
  |check_board_complete(), check_line(), and check_match() are conditional evaluators that are targeting selectors before their next moves to see if the game is done. 

  ```
```javascript
const check_match = () => {
  for (i = 0; i < 9; i += 3) {
    if (check_line(i, i + 1, i + 2)) {
      document.querySelector(`#block_${i}`).classList.add("win");
      document.querySelector(`#block_${i + 1}`).classList.add("win");
      document.querySelector(`#block_${i + 2}`).classList.add("win");
      return play_board[i];
    }
  }
  for (i = 0; i < 3; i++) {
    if (check_line(i, i + 3, i + 6)) {
      document.querySelector(`#block_${i}`).classList.add("win");
      document.querySelector(`#block_${i + 3}`).classList.add("win");
      document.querySelector(`#block_${i + 6}`).classList.add("win");
      return play_board[i];
    }
  }
  if (check_line(0, 4, 8)) {
    document.querySelector("#block_0").classList.add("win");
    document.querySelector("#block_4").classList.add("win");
    document.querySelector("#block_8").classList.add("win");
    return play_board[0];
  }
  if (check_line(2, 4, 6)) {
    document.querySelector("#block_2").classList.add("win");
    document.querySelector("#block_4").classList.add("win");
    document.querySelector("#block_6").classList.add("win");
    return play_board[2];
  }
  return "";
| These are the actual lines of code that check for the lines to be completed go check for the win and add the class of win. It looks like a decent chunk of code cuz we've got to check for every single combination, of which there are quite a few.
  ```

```javascript
  const check_for_winner = () => {
  let res = check_match()
  if (res == player) {
    winner.innerText = "You Win!!";
    winner.classList.add("playerWin");
    board_full = true
  } else if (res == computer) {
    winner.innerText = "YOU LOSE!!";
    winner.classList.add("computerWin");
    board_full = true
  } else if (board_full) {
    winner.innerText = "STALEMATE!";
    winner.classList.add("draw");
  }
};
|This group of good first creates a variable as an arrow function to begin a set of conditional statements that run through some circumstances to evaluate and declare a winner.
Conditional statements and booleans created with dom manipulation.
```

```javascript
const render_board = () => {
  board_container.innerHTML = ""
  play_board.forEach((e, i) => {
    board_container.innerHTML += `<div id="block_${i}" class="block" onclick="addPlayerMove(${i})">${play_board[i]}</div>`
    if (e == player || e == computer) {
      document.querySelector(`#block_${i}`).classList.add("occupied");
    }
  });
};
this block of code is what lets the gameboad read that the players are taking turns by occupying the boxes on the 9 square grid. The if statement checks if either the player or the computer is the one occupying the space, for which the same class is given to the box. 
```

```javascript
const game_loop = () => {
  render_board();
  check_board_complete();
  check_for_winner();
}
We are just using this code to call and check if we're going to be be making a move. We declare a variable as an arrow that function with 3 functions called nested inside of it. 
```
```javascript 
const addPlayerMove = e => {
  if (!board_full && play_board[e] == "") {
    play_board[e] = player;
    game_loop();
    addComputerMove();
  }
  we add this code allowing the player to move on the condition that the board is not full. We add the game_loop() function, and for the computer to move,  checking again for the condition of the board being !board_full (NOT FULL)
  ```

  ```javascript
  const addComputerMove = () => {
  if (!board_full) {
    do {
      selected = Math.floor(Math.random() * 9);
    } while (play_board[selected] != "");
    play_board[selected] = computer;
    game_loop();
  }
};
Here is the condition, again, of checking for room to be available before allowing a player to make a move (in this case the computer). Math.random on the available squares on the 9 block grid is the set up used to allow the computer options to decide its next move. 
```

```javascript
const reset_board = () => {
  play_board = ["", "", "", "", "", "", "", "", ""];
  board_full = false;
  winner.classList.remove("playerWin");
  winner.classList.remove("computerWin");
  winner.classList.remove("draw");
  winner.innerText = "";
  render_board();
};
This code sets the block array to empty to initialize the restars.
The .classList.remove property is targeting the elements as objects and removing their game-decisions based messages (Player win, computer win, draw) before using winner.innerText to make the message empty, restarting the game. 

```