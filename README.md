# Assignment 5: Happy Holidays

## Due: Tuesday Nov 26th, 11:59pm

**Important**: because the Thanksgiving break follows this due date, we're "ignoring" Thursday when computing lateness. So, Wednesday 27th at 11:59pm is one day late, Fri 29th at 11:59pm is two days late, Sat 30th at 11:59pm is three days late, and Sun 31st at 11:59pm is four days late (and the **last day you can submit**).  I will repeat that:  you may not submit the assignment after Sunday night.  The TAs have exams so on, and need time to grade.   Emergencies that occur **after** the original due date (Tuesday 26th) will not be grounds for an extension past Sunday. 

**Update**: we will only be deducting 2.5% per day late, instead of 5%, to allow people who want or need to use part of the Thanksgiving break to do so without a huge penalty.  The official due date is still Tuesday the 26th.

You will notice there is no sample code for this assignment.  You can structure the assignment as you wish.  The only requirements are discussed at the bottom of this document, and are meant to simplify the job of the TAs (e.g., you should name the top-level page a5.html, and follow a few simple instructions, so the TAs know how to run it).

You can use WebGL, or use another library on top of WebGL, such as http://threejs.org, http://www.babylonjs.com, etc.  However, if you use a higher level library, you will be required to pick one of the bonus parts and implement it as part of your assignment (since the higher level library simplifies many of the tasks you need to do, especially picking/selection). The assignment is designed such that you can do it using WebGL alone, with the techniques and tools you already know.  But, if you want to learn a more powerful 3D library, this would be a good opportunity.

## Assignment Details

For this project, you will make an interactive holiday "mobile", with letters hanging from strings of different lengths from the top of the screen.  The letters should be evenly spaced across the screen, and at random heights between 1/4 and 3/4 the height of the screen (i.e., the middle half of the screen). Each letter should be "connected" to the top of the screen with a line (it's "string"). At a minimum, each letter should be represented by a single quad, but you can make the letters more elaborate if you want. Each letter should be tilted slightly to the right or left (randomly) as seen by the viewer, so that the pattern is visually interesting.  The letters could be "just the letter" (e.g., a transparent texture) or could be a solid square with the letter in it, the choice is yours.

You are free to render letters in any way you want. For ideas and guidance on how to render text, such as using textures, start with the examples in webglfundamentals.org.  But, you are free to also consider other approaches, such as generating textures on the fly from web fonts as shown in https://github.com/mikolalysenko/gl-render-text, creating meshes from SVG character (https://css-tricks.com/rendering-svg-paths-in-webgl/), or adapting more refined solutions (https://www.eventbrite.com/engineering/its-2015-and-drawing-text-is-still-hard-webgl-threejs/). You are free to use a library to generate the text images (as in the gl-render-text example), or simply create the textures you want by hand (for example, using photoshop) as done in webglfundamentals.org (the advantage of the latter is that you can create a rectangular texture for each letter that looks exactly like you want, with any additional decorations or styling you care to add, but it may require more up-front work).

The key part of this assignment, however, is that the mobile must be interactive:

* the message should be taken from the keyboard.  Your scene should start with no text, but should have instructions that tell the user that they can type any letters to create a message, how to reset the message text, and what the maximum number of characters are (if any). As letters are typed, they are added to the message.  You should accept (at least) letters and spaces, but can also accept other characters if you want.  As characters are typed, they should be added such that the message is centered on the screen.  

* the user should be able to click on the letters.  When they do, the letters should spin, with the speed and (thus) the amount they spin based on how far from the horizontal center they click (click near the left or right edge to spin multiple times, click near the middle to spin just once). The letter should always end up facing forward again, and should decelerate smoothly from it's initial speed. So you should look at the distance from the center, decide how many times to spin, and start the spin at the right speed such that it will end up facing forward.  One way to handle the deceleration is to use part of a sin() wave (perhaps from 90..180 degrees) to start at full speed and end at zero speed, with the total amount of rotation being spread through that range).   You can use either approach to selection we discussed in class (ray casting, which in this case would be a ray-polygon intersection, or the render buffer technique).

* you can allow the user to click again on a spinning letter, or not allow a letter to be clicked on again until it stops.  Your choice.

* you must allow all the letters to be spinning at the same time.  So make sure you associated the spinning state with each letter, do not just have one set of global state such that only one letter can be spinning.

* when the user types a letter, a sound should play.  When they click on a letter with the mouse, a different sound should play.  (you might consider using a wrapper library like [howler.js](http://goldfirestudios.com/blog/104/howler.js-Modern-Web-Audio-Javascript-Library) which has a TSD wrapper already built, instead of using the web audio APIs directly).

(A note about TSC types: types for thousands of Javascript libraries are in https://github.com/DefinitelyTyped/DefinitelyTyped and can be installed using npm. In this case, `npm install --save-dev @types/howler` will install the howler.js typings.  The `tsc` compiler should see any typings installed this way.)

For input, do not create a text entry box, rather use the keyboard events (e.g., onkeydown) to capture keypresses.  

The basic assignment does not have to adjust the size of the letters based on how much the user types, but can use a fixed size.  However, the letters should be sized and spaced such that the message "Happy Holidays" can be displayed. 

For rendering lines, look up the documentation for rendering gl.LINES (analogous to rendering triangles with gl.TRIANGLES).  [Here's a example](http://www.codeproject.com/Articles/594222/LineplusinplusWebGLplusandpluswhyplusyouplusgonnap) with some code.

You must also clearly identify what you did (summarize how you solved each element of the basic assignment, along with what bonus parts you did and how the TA can see them in action if needed) in text on the HTML page under the 3D canvas element.

## Grading

This assignment will be graded as follows (out of 30):
* 6 points for rendering text characters (including input and sound)
* 3 point for proper horizontal spacing (that adjusts if the window is resized horizontally)
* 3 point for proper random vertical positioning (we suggest you have your window be fixed sized vertically as in the examples up to now, but if you resize the letters should adjust accordingly)
* 3 point for drawing lines for the "strings"
* 3 point for correct text input
* 6 points for selection and spinning the letters at all (including sound)
* 3 point for properly adjusting the speed and amount of spin based on where on the letter the user clicks.
* 3 point for overall program and output appearance: reasonable title and instructions, and having the 3D window respond appropriately to window resize, clearly identifying what you did.

As noted above, if you are using a higher level library, such as three.js, you will also need to do one of the bonus options as part of the main assignment.  In that case, the basic assignment will be graded out of 24 (instead of 30), and the first bonus being used to bring the score up to 30.  Please make it clear (in description on the html page) which of bonus item you are doing as part of the main assignment.  

## Leveraging code from the internet

If you copy any code from the internet (including from sites we have been using, such as webglfundamentals.org or threejsfundamentals.org), please document it. Any code that helps you with accomplishing general 3D rendering (e.g., setting up state, etc) is fine. Code that specifically implements parts of the assignment are not fine.  If in doubt, ask.  (I suspect, for example, that any code on webglfundamentals.org is fine -- it is probably ok to start with one of their examples.  Again, just document it).

## Bonus

Unlike previous assignments, you may do additional work for bonus points.  Each of the bonus options can earn up to 6 points (4 points for meeting the requirements, up to 2 more points for particularly aesthetically interesting/pleasing results), and you may do at most 3 of them.

Possible bonus options include:

* Swinging letters. Each of the letters should be swinging very slightly (so they don't look static).  They should not be synchronized or the same speed.  You can make them swing by using the top point of the string as a rotation point and computing the bottom point of the string (where the letter is) by rotating a point the length of the string around this top point.  As with other animations, by using sin() and a function of time you should be able to slowly swing the letters.  When the letters are clicked with the mouse, in addition to rotating as described above, the letters should swing a bit more while spinning, settling down to their default swing as the rotation stops.  

* Snowflakes or leaves or any falling holiday things.  You should have a large number of holiday-oriented things falling in the background behind the mobile, moving in a convincingly random way as they fall (i.e., by leveraging randomization techniques like Perlin noise), with flakes of different sizes as they recede in the distance.  There are many examples of creating snow in OpenGL, WebGL and three.js on the net that you can learn from, if you want.  Do NOT just copy one into your code without modifying it in some meaningful way.

* Background.  Put a complementary image in the background of the scene, and have it move as the mouse moves over to create a low-key motion effect. One way to do this would be to have the image be larger than the screen, and when the mouse is to the left/below the center, move the image proportionally right/up a small amount (and vice-versa).

* Animated entrance/exit for the letters.  In the basic assignment, the letters can appear and move to new positions immediately when new letters are added, and disappear when the scene is reset.  In this extra credit, the letters would animate into the scene (e.g., perhaps they drop in from the top in their desired position, while the other letters slide to the left;  resetting might have them all slide off screen).  Care must be taken with this extra credit is dealing with overlapping animations (e.g., I type very fast, so the letters are falling and moving;  I clear the letters and start typing, so new letters are coming in while others are leaving).

* Pagination.  Allow a much larger number of characters to type by having the letters start at a large size, and scale down to smaller letters as the screen is filled.  As more are typed, additional rows are created.  You do not have to support an infinite amount of text: pick a minimum letter size, and maximum number of lines (even two lines is sufficient). 

## Submission

You should submit your entire code directory (WITHOUT the ```node_modules``` directory generated by npm) via github, as before.  Please use a reasonable `.gitignore` (look at the ones in your previous assignments) that at least ignores the ```node_modules``.  

Make sure you submit any assets, such as image files you load in as textures.  Do not refer to resources elsewhere on the web; copy them into your project directory.

Your web page should be titled ```a5.html``` and your main .ts file should be ```a5.ts```, so the TAs know where to look.    

You should set up your project to build as the fourth assignment, and should let the TAs cd into the directory and type:

1. cd into the directory and run ```npm install```

2. compile with ```tsc``` 

3. run whatever command they want to start a server on the project directory 

3. open and view the web page ```localhost:8080/a5.html``` (or whatever port their server is using)

(We are asking you to run the server, even if your solution doesn't need it, so the TAs have a simple and consistent way to build and test each assignment).
