# Imperial Tetris
Project 1 
A demo of the Imperial Tetris Game running:
![](https://media.giphy.com/media/or2gRb0oyZQymPetZP/giphy.gif)


## Technical Requirements
*Technical Requirements
Your app must:
* Display a game in the browser
* Switch turns between two players, or have the user play the computer (AI or obstacles)
* Design logic for winning & visually display which player won
* Include separate HTML / CSS / JavaScript files
* Stick with KISS (Keep It Simple Stupid) and DRY (Don't Repeat Yourself) principles
* Use Javascript for DOM manipulation
* Deploy your game online, where the rest of the world can access it**
* Use semantic markup for HTML and CSS (adhere to best practices)

## Concept
I wanted to create my own version of a Tetris game. When I was young, that's pretty much what I enjoyed playing on the Nintendo Game Boy.

Screenshot of the main screen: Instructions, Start/Pause, and Reset Button.
![](https://i.imgur.com/SZBAMuw.jpg)

## Music
I went with the main original Tetris theme song. Listening to it while I play, gives me good nostalgic childhood memories.☺️ You can hear it when you press the START/PAUSE button.

## Instructions
The aim in Tetris is pretty simple; you bring down blocks from the top of the screen. You can move the blocks around, either left to right and/or you can rotate them. The blocks fall at a certain rate, but you can make them fall faster if you’re sure of your positioning(just keep pressing down on the Arrow Down key). Your objective is to get all the blocks to fill all the empty space in a line at the bottom of the screen; whenever you do this, you’ll find that the blocks vanish and you get awarded some points. For my version, this will be a never-ending game. So you can play until you drop! 😂

# How To Install
* Click on the link here --> https://sharleneimperial.github.io/Tetris-Game-Project-1/
* You can ⑂ Fork and Clone this repository to your local machine.
* Open the `index.html` in your internet browser to play (I highly reccomend using Google Chrome).
* Or you can use a Live Server plug-in.

## How To Play
Here's a video capture of the instructions
![](https://i.imgur.com/BbKwUmc.mp4)

* ⬅️ Move Left - Arrow LEFT key 
* ➡️ Move Right - Arrow RIGHT key
* ⬇️ Move Down - Arrow DOWN key
* ⬆️ To Rotate Tetro Pieces - Arrow UP key

## Blockers
Yes, I did come across some minor bugs, but it is what makes coding so fun and yet challenging at the same time.

## Language
* JavaScript
* HTML 5
* CSS

## Here Are Some Of My CODE SNIPPETS

1. Setting the variables for the colors of each Tetropieces in order below:
```javascript
const tetColors = [
    'pink', 
    'white',
    'skyblue',
    'green',
    'yellow'
]
```

2. Setting variables for The Tetro Pieces by colorClass and shapes of each rotation of the piece in each array.
```javascript
    const zTetroPiece = {
        colorClass: 'zPiece',
        shapeArray: [
            [0, width, width+1, width*2+1],
            [width+1, width+2, width*2, width*2+1],
            [0, 10, 11, 21],
            [width+1, width+2, width*2, width*2+1]
        ]
    }

    const tTetroPiece = {
        colorClass: 'tPiece',
        shapeArray: [
            [1, width, width+1, width+2],
            [1, width+1, width+2, width*2+1],
            [width, width+1, width+2, width*2+1],
            [1, width, width+1, width*2+1]
        ]
    }

    const iTetroPiece = {
        colorClass: 'iPiece',
        shapeArray: [
            [1, width+1, width*2+1, width*3+1],
            [width, width+1, width+2, width+3],
            [1, width+1, width*2+1, width*3+1],
            [width, width+1, width+2, width+3]
        ]
    }

    const lTetroPiece = {
        colorClass: 'lPiece',
        shapeArray: [
            [1, width+1, width*2+1, 2],
            [width, width+1, width+2, width*2+2],
            [1, width+1, width*2+1, width*2],
            [width, width*2, width*2+1, width*2+2]
        ]
    }

    const oTetroPiece = {
        colorClass: 'oPiece',
        shapeArray: [
            [0, 1, width, width+1],
            [0, 1, width, width+1],
            [0, 1, width, width+1],
            [0, 1, width, width+1]
        ]
    }
```
3. Drawing out the Tetropiece:
```javascript
    function drawTet() {
        current.forEach(index => {
            grids[currentPosition +index].classList.add(activePiece.colorClass);
        })
    }
```

    Undrawing the TetroPiece:
```javascript
        function undrawTet(){
            current.forEach(index => {
            grids[currentPosition + index].classList.remove(activePiece.colorClass)
        })
    }
```
4. Here I wanted to create a little something extra to my game. Adding a small box (Next Up `.smallGrid div` box)    that shows which piece is coming up next.
Using the `querySelectorAll`, want all the divs inside the div with the class `.smallGrid` div.
Setting the `const showWidth` at 4 will see how big the smallGrid is and `const showIndex` setting the index at 0.
Then a function to show the shape in the smallGrid box.

```javascript
    const showGrids = document.querySelectorAll('.smallGrid div') 
    const showWidth = 4 
    const showIndex = 0 

    function showShapeTet() {
        // Remove any of a tetroPiece from the whole grid
        showGrids.forEach(grid => {
            grid.classList.remove('tetropiece')
            grid.style.backgroundColor = ''
        })
        nextUpTetroPieces[otherRandom].forEach( index => {
            showGrids[showIndex + index].classList.add('tetropiece')
            showGrids[showIndex + index].style.backgroundColor = tetColors[otherRandom]
        })
    }
```
```html
In HTML:
    Created a total of 16 divs for the class "smallGrid", (Next Up:) box in JS
    <h2 class="nextUp">Next Up:
      </h2>
    <div class="smallGrid">
      <div></div> 
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div> 
    </div>
     </div>
```
5. The freezeTet function:
    Checking to see of the next space below is `occupied`.
    Then it will create a new tetroPiece falling.
```javascript
    function freezeTet() {
        if(current.some(index => grids[currentPosition + index + width].classList.contains('occupied'))) { 
            current.forEach(index => grids[currentPosition + index].classList.add('occupied')) 

            random = otherRandom
            otherRandom = Math.floor(Math.random() * theTetroPieces.length) 

            activePiece = theTetroPieces[random];
            current = activePiece.shapeArray[currentRotation];
            
            currentPosition = 4
            drawTet() 
            showShapeTet()
            addTetScore() 
            gameOverTet()
         }
    }
```
6. The functionality to the startButton :
    The `startButton` is attached to the `addEventListener`. 
    When the button is pressed, then the tetroPiece is drawn.
    Invoking the `goDown` every 1000 miliseconds.
    Then the next random shape will show in the `smallGrid` thus will invoke the `showShapeTet` function here.
```javascript
    startButton.addEventListener('click', () => { 
        if (timerId) {
            clearInterval(timerId)
            timerId =  null 
        } else { 
            drawTet() 
            timerId = setInterval(goDown, 1000) 
            otherRandom = Math.floor(Math.random()*theTetroPieces.length) 
            showShapeTet()
            
        }
    })
```
7. Adding the score:
    Here, I used the `for loop` method, defined the `const row`.
    If every grids in the defined row contains a div with the class of occupied and is true, then it will add 10 points to the score. Thus it will show the score `tetScore`.
    And `forEach` item of the row, removing the class `occupied`.
    Then removing the row using the `splice` method.
    And lastly, append the new grids for the grid.

```javascript
    function addTetScore() {
        for (let i = 0; i < 199; i +=width) { 
            const row = [i, i+1, i+2, i+3, i+4, i+5, i+6, i+7, i+8, i+9] 

            if(row.every(index => grids[index].classList.contains('occupied'))) { 
                tetScore +=10 
                score.innerHTML = tetScore 
                row.forEach(index => { 
                    grids[index].classList.remove('occupied')
                    
                })
                const removeGrids = grids.splice(i, width) 
                removeGrids.forEach(cell => {
                    cell.classList.remove('zPiece','tPiece', 'iPiece', 'lPiece', 'oPiece');
                })
                grids = removeGrids.concat(grids)
                grids.forEach(cell => grid.appendChild(cell)) 
            }
        }
    }
```
8. And Finally, here is the: Game Over function:
    If the current tetroPiece position contains the class of `occupied` then it's Game Over. 
    Then it will be shown Game Over in the Your Score: section. 
    The `timerId` is cleared, when the `goDown` function comes to a stop.
```javascript
    function gameOverTet() { 
        if(current.some(index => grids[currentPosition + index].classList.contains('occupied'))) {
            score.innerHTML = 'Game Over'
            clearInterval(timerId) 
            aud.pause(); 
        }
    }
    })
```
Screenshot of Game Over(when all pieces are stacked to the top)
    ![](https://i.imgur.com/Lmwp02g.jpg)








