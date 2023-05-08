Download Link: https://assignmentchef.com/product/solved-two-part-c-tetris-game-startup
<br>
Part I – Set up the Bucket

Create Tetris bucket

Bucket will be a 2-D array of char of 25 x 12 dimension.

Fill the left border (column 1), right border (column 12), and bottom border (row 25) of the bucket with any char that you like to create the border with. Remember, the array index is ‘1’ lower than the actual # of columns. This can be your “initializeBucket()” function. Fill the other cells with empty string ‘ ‘. You know that, to go over a 2-D array you need two nested for loops. Right? You also need conditional statements.

Display the bucket in a game loop. How do you do that? You use two for loops and use a “cout….”. You can name the function “displayBucket()”.

Remember the top and left most location of the console is (0,0). So, if you want to draw from the top-left most, you call the function this way, “setCursorTo(0, 0);”. Then do your ‘cout &lt;&lt; “etc etc …”&lt;

<table border="1" cellspacing="0" cellpadding="5">

 <tbody>

  <tr>

   <td>void setCursorTo(int x, int y){HANDLE handle;COORD position;handle = GetStdHandle(STD_OUTPUT_HANDLE);position.X = x;position.Y = y;SetConsoleCursorPosition(handle, position);}Void main(){setCursorTo(0, 0);cout &lt;&lt;“etc etc …”&lt; }</td>

  </tr>

 </tbody>

</table>

Here is how your bucket should look like after you finished the step. Notice, you have left border, right border, and bottom border, and everything inside is empty string.<img decoding="async" alt="N207-Module_04-Tetris_Bucket.png" data-recalc-dims="1" data-src="https://i0.wp.com/content.learntoday.info/N207_Fall_14/site/Media/N207-Module_04-Tetris_Bucket.png?w=980" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/content.learntoday.info/N207_Fall_14/site/Media/N207-Module_04-Tetris_Bucket.png?w=980" alt="N207-Module_04-Tetris_Bucket.png" data-recalc-dims="1">

 </noscript>

Part II – Drop the Shapes into the Bucket

To represent the Tetris shapes, you can create a Class called “TetrisShape”. In the class, declare a 2-D array of chars that is 4×4 in size (you could also use 4×2 but that would require different algorithm). Call the array “shapeArray”. For convenience, declare it as public (but, it should not be your practice when you work in the software industry). You might need more dimensions for the array if you want to statically assign (hard code) all the shape rotations (3-d) for all the shapes (4-d). In this example, the rotation of the shapes is done by value swapping in the 4×4 array.

Now, populate or initialize the “shapeArray”. There are three (3) options for doing this:

<strong>Option 1:</strong> Add a function in the class (call it “populateShapeArray(int shapeType)”), that will take an integer which will denote the type of shape.

<strong>Option 2:</strong> Use a non-default constructor. In this case, when you create an object, you will take an integer as the constructor argument, which will denote the type of shape, as shown below.

<table border="1" cellspacing="0" cellpadding="5">

 <tbody>

  <tr>

   <td>TetrisShape currentShape = new TetrisShape(shapeType);// shapeType is an int</td>

  </tr>

 </tbody>

</table>

<strong>Option 3:</strong> Use a setter “setShape(int shapeType)” function.

Regardless of which option you chose above, you would use a switch statement to assign the 4×4 array values for the specific shape. For example, for ‘L’, it can be something like the following:

<table border="1" cellspacing="0" cellpadding="5">

 <tbody>

  <tr>

   <td>shapeArray[0][0] = ‘ ‘; shapeArray[1][0] = ‘X’; shapeArray[2][0] = ‘ ‘; shapeArray[3][0] = ‘ ‘;shapeArray[0][1] = ‘ ‘; shapeArray[1][1] = ‘X’; shapeArray[2][1] = ‘ ‘; shapeArray[3][1] = ‘ ‘;shapeArray[0][2] = ‘ ‘; shapeArray[1][2] = ‘X’; shapeArray[2][2] = ‘X’; shapeArray[3][2] = ‘ ‘;shapeArray[0][3] = ‘ ‘; shapeArray[1][3] = ‘ ‘; shapeArray[2][3] = ‘ ‘; shapeArray[3][3] = ‘ ‘;</td>

  </tr>

 </tbody>

</table>

<table border="1" cellspacing="0" cellpadding="5">

 <tbody>

  <tr>

   <td>bucket[i+shapeTopLeftX][j+shapeTopLeftY] = localTetrisShape.shapeArray[i][j];</td>

  </tr>

 </tbody>

</table>

You are actually imposing the shape values on to the bucket.

Always keep record of the top left corner location (x,y dimensions) of the shape that is falling. This record will indicate where to draw the shape in the bucket after the shape moves. Initially, the location should be, (6, 0), which is the top middle of the bucket. Store the coordinates in the “TetrisShape” class as shapeTopLeftX and shapeTopLeftY. Note, x changes horizontally, and y changes vertically.

In this step you will generate one shape. To accomplish this, in the main() function, before the while loop (game loop), do the following:

Generate a random number from 0 to 6.

Use one of the options presented in step 2 above to create a TetrisShape object.

Create a global function called “updatebucket(TetrisShape localTetrisShape)” to populate the bucket with values of the “shapeArray”. Here, you will use two nested for loops to go over the shapeArray of 4×4. You need to provide the TetrisShape object (created in step ‘4b’ above) to the function as an argument in order to access its shapeArray. Inside the loop, you will do this.

Call the “updatebucket(TetrisShape localTetrisShape)” function from main() using the object created in step 4b.

Display the bucket.

Inside the while loop (game loop), as the shape falls, the value of y will increase. In order to accomplish this you will have “newShapeTopLeftY = shapeTopLeftY + 1;” so that the shape falls one cell below. Notice that you are storing the new y value in another variable because you need both the old and the new values.

Clear (assign spaces to) the current position values of the shape in the bucket using the “old” shapeTopLeftX and shapeTopLeftY. This will ensure that you do not leave any trail of the shape.

Call the “updatebucket(TetrisShape localTetrisShape)” function with the “new” shapeTopLeftX and shapeTopLeftY values. This will ensure the shape will be displayed in the new location (newShapeTopLeftX, newShapeTopLeftY).

Display the bucket. The shape is displayed in the new location of the bucket.

Store the new shapeTopLeftX and shapeTopLeftY values to the old shapeTopLeftX and shapeTopLeftY values to get ready for the next loop.

Sleep for a while to slow down the game.