# Block Dodger #

Zheng Tang
Lubawy, Drew

# Introduction #

This is a verilog designed video game and implemented using DE2-115, PS/2 keyboard and VGA screen. Object of this video game is to build a block that can control, and other blocks that can bouncing around, and control one block to avoid the other ones as long as you can.

# Details #

## VGA signal ##

VGA background information could be found in http://martin.hinner.info/vga/ and the timing information for different resolutions could be found in http://tinyvga.com/vga-timing. We have struggle a lot to build our own vga, but failed due to the misunderstanding of VGA\_CLK output meaning in VGA signal. Eventully with the help Ehret Alan and his code of VGAhttps://code.google.com/p/julia-set-generator/source/browse/#git%2Ftest_projects%2Fvga_800x600_example, we have our VGA signal done. Then by using and manipulate the pixel count and line count of each frame, we could draw thing we want.
Dr. John S. Loomis code for drawing stuff was really helpful, http://www.johnloomis.org/digitallab/, it can draw picture and letter by using the RAM, using the RAM to generate each locations for each pixel, and specific how those pixel will act at the addressed location. It is a really good example of how to initial the RAM with one frame, but it doesn't teach how to change those data to do animations as we wanted, and the address for each pixel is too much for our purpose of using.

## Drawing block ##

After the VGA was done, we almost hard code and assign the boundary by using pixel count and line count to make VGA draw blocks at specific range. We have total 25 blocks draw. We could build a boundary generator that generate the random locations for block,but it need more time.

## Block movement ##

Adding the movement of control block is simple to say that increment constant-a (different a will result in different speed) of the boundary of block at each clock cycle when specific button was hit. The free move block need 3 more things need to consider, the speed for horizontal and vertical direction, and the directions, and how the directions change when hit the boundary.We initial and hard core the speed, and direction, and simply tell the block to flip the horizontal or vertical direction when hit horizontal or vertical wall of boundary. This method sort of work for our design, but it has many flaws as the simulation for uniform movement.

The cause of flaws can be conclude by 2 reasons, discontinues of the space(pixels) and discontinues of the time(we change the boundary at each frame). A sharp angle of the block direction will result in unacceptable large speed and therefore obvious position jumping. Another algorithm of implement space and time and their relationship between the pixels may needed to fix this problem, but is needs time and the present method just work for our design.

## Block collision ##

The collision is detected by if one of the boundary of those free move block is in the boundary of the control block. So a large if statement.

## Timer ##

The timer on the screen is used to displace the score that how long the player has played. We made the timer as a digital clock, assign the boundary for each 7-segment on the screen, and control on or off by one register. And this problem eventually become the early lab for 7-seg decoder but with time input.And the code that case statement for 7-seg decoder, we used part of Dr. John S. Loomis's P/S2 keyboard code.

## P/S2 keyboard ##
You can find the general keyboard signal information at http://retired.beyondlogic.org/keyboard/keybrd.htm.
The keyboard send ASCII code to the host, including pressed key and break key. Due to the complex of the keyboard communication between the host, we just used other people's code. After several testing, we find Dr. John S.Loomis's P/S2 keyboard code is best for us http://www.johnloomis.org/digitallab/ps2lab1/ps2lab1.html
This code recorded the 32 bit of the keyboard transmitted ASCII data, in this way we can add the algorithm to see if a key is hold or break, also works for holding multiple key as releases one of them. In this we we could move the block in 8 direction freely.

# Result #
They work of the time is huge but less efficiently(it is above 100 hours , because we almost begin to learn everything as we do the project, and we are not that smart)
Here is the video link:[http://youtu.be/4S3fwqCc-yI](.md)

## Citation for using code ##
Ehret Alan VGA driver https://code.google.com/p/julia-set-generator/source/browse/#git%2Ftest_projects%2Fvga_800x600_example
Dr. John S.Loomis's P/S2 keyboard code http://www.johnloomis.org/digitallab/ps2lab1/ps2lab1.html


