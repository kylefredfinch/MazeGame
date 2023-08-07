# MazeGame
This is a randomly generated maze where the objective is to manipulate the ball through the maze and collide with the square.  I have relied on the Matter.js engine to easily create an environment of shapes. 

One of the main challenges was understanding the logic to how the maze was going to be randomly generated. I created this with a function I called randomWalk(), and the idea is that at any given cell in an nxn grid, there is a choice for the path to one of the neighboring cells. And when the randomWalk travels through to one of the radnomly selected cells, that wall should be open. I have shuffled these choices to create a random pathway with the shuffle() funciton:

const shuffle = (arr) => {
    let counter = arr.length;

    while (counter > 0){
        const index = Math.floor(Math.random() * counter);

        counter--;

        const temporary = arr[counter];
        arr[counter] = arr[index];
        arr[index] = temporary;
    }

    return arr;
}

Now, any array I pass throough shuffle() will return a new shuffled array, creating the randomness to this application. The neighboring cells for which the choices are to be shuffled can be seen by neighbors variable:

const neighbors = shuffle([
        [row - 1, column, 'up'],
        [row, column + 1, 'right'],
        [row +1, column, 'down'],
        [row, column -1, 'left']
    ]);

With shuffle being applied to this array, we have a random walk coming into fruition. I added the descriptive values of 'up', 'right', 'down', and 'left' to better inform the next part of the code, which is to remove the wall should the random walk decide to go through to the randomly selected cell: 

 if (direction === 'left') {
            verticals[row][column - 1] = true;
        } else if (direction === 'right') {
            verticals[row][column] = true;
        } else if (direction === 'up'){
            horizontals[row - 1][column] = true;
        } else if (direction === 'down'){
            horizontals[row][column] = true;
        }

Here, the boolean of 'true' signifies if a wall is open or not, and therefore signifying if you can travel through it. With how the code has been set up there should be no cells which are blocked off. 

Once the logic of the game was set up, it was mainly styling problems which came to light. For example, how to create walls and where their center points should be to relate to the correct wall in logic. 



Things that I am not happy with and looking to modify:

- The functionality of moving the ball through the maze is quite difficult to get the hang of. In matter.js there is two options with the 'gravity' setting which is no gravity, and so the ball will always fall to the bottom, and no-gravity and so you have a sense of difficulty when trying to move the ball through this floating environment. I was thinking about trying to modify the movement to the ball so that each keydown will translate the ball to the corresponding cell. This may be clunky to look at but I think it will improve user experience.

- There is currently no 'next thing' to do. When you win, I am looking to include a 'next level' button which can increase the number of cells in the grid (making it more detailed, and hence more difficult). Potentially once the user goes through a certain amount of levels they unlock something different (like a new color selection on the ball).
  
- It might be cool to add a home page before you enter the game. Rather than simply starting on a maze level (which is hard-coded), having a home default page is more realistic. This is where you could have an option page and the user can specify themselves a few details - for example, how they prefer to manipulate the ball, some may like gravity, some may not, so that could be a user selected option?).
  
- Instead of hard-coding a the horizontal and vertical cells in the game, I would like to create some configuration on an simple 'Level 1' setting which will mould to the window of the users, once this has been set you can go through each level by increasing the rows and columns in the grid by 1 and increasing the difficulty.
  
- It would be cool to have a different way of signalling the end of a level each time through (e.g. turning gravity on and off, flashing colors on the walls, etc.).



I think the next thing I have to do is put all this code into some reusable state which I can rely upon for the creation of multiple levels. 
