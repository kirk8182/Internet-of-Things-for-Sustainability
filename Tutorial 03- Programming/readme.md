# Introduction to Programming with Arduino C/C++

## Introduction

### Topics for this tutorial
  1. Learn the basic format of C code
  2. Learn the structure of a basic arduino file
  3. Variables and types
  4. Conditionals and loops (if, else, while)

## Explanation
This tutorial will be a basic crash course into the fundamentals of programming your own arduino programs to run on your Galileo board. We will take a look at the code used in the previous Nightlight program, and work on examples similar to that code. The goal is to learn how to write and read simple arduino programs for our own Galileo board. We will cover the structure of an Arduino program, how to declare and use variables, and conditional statements and loops. 
An important note is that the code we will be using for our Arduino programs mostly follows the syntax of C, C++, and any languages like them, along with its own Arduino flare. Each piece of code will be shown below and hopefully explained in an easy to understand way.

## Required Materials
  1. Intel Galileo and Grove shield
  2. Arduino IDE
  3. Grove button
  4. Grove light sensor
  5. Grove LED

## Arduino Program Structure
### Programming Concepts
We will start by opening up our Arduino Interactive Development Environment, or IDE for short. After opening the Arduino software, we should start a new file by clicking the blue New File button at the top, which will take us to a screen like this. 
![Opening IDE](https://cloud.githubusercontent.com/assets/22579849/23933974/52b7030c-08ff-11e7-945e-995b8be870ee.PNG)
To begin programming our own first arduino program, we need to understand the major components to include in a .ino file. There are two key parts that we need to add to our own program, and fortunately, the IDE has supplied us with both of those things, but empty.  
First off, the programs that we will be creating throughout this workshop follow the C programming format, which you will hopefully learn by observing the programs in the workshop. The most important rule of programming, is that the code you type in must fit a certain format. Many errors that you will face early on occur because of a missing letter, number or other symbol. Think about the following line of C code:

>  int my_favorite_number = 4;

There are quite a few things going on with this snippet of code. In english, it looks like I am saying that my favorite number is 4. This is close to what it means in the code. The first element of that line, "int", is short for integer, which is any whole number with no following decimal places. Used in code, this states that the word coming after it is going to be a new variable, which is an element used by the program. For each variable name, the type of it can only be specified once, so only include the int for each new variable once. This sets a place in memory and inserts the value 4 into it, so if we type anywhere in the code the variable "my_favorite_number", it will take out that word and insert a 4 in its place. This is critically important to programming when you consider that you are able to adjust the contents of the variable anywhere in the code. Also to note is that we can change the name of the variable to anything we want, as long as it consists of only letters, underscores, and numbers that aren't at the beginning of the variable name. The semicolon at the end is specific to C, and usually declares the end of a line of code. 

If we look at our Arduino IDE, we will see that there is a line called "void setup() {", and one called "void loop() {". As you can see, those lines don't end with a semicolon, and instead end with a curly brace, which signifies that all of the code within the left curly brace { and right curly brace } are a part of the section named before it, such as setup, which we will discuss next. 

### Galileo Program Setup
When the program is uploaded to the Galileo board, the first thing that runs is setup. An important thing to notice is that a double slash mark, or //, in the arduino code, denotes a comment and everything past the slashes will have no impact on the code. The code looks like this:

>  void setup() {
>  // put your setup code here, to run once:
>  
>  }

As it says in the comment, this block of code will run once. It is very important to define the various pins on the Galileo shield as either output or input through the use of the pinMode() function. The pinMode() function, as well as any other function, takes a number of input values which are within the parenthesis, points to a larger block of code, and when you use the function call such as pinMode(), it uses the inputs and runs all of the code that it points to. And unless you are building functions, its not that important to know what goes on in one. For us, pinMode() just sets up the connector on the shield to either send information out (output), or to receive information from a source (input). We will start off easy, and add the following line of code on its own line between the two curly braces of the setup function:

>  pinMode(8, INPUT);

This pinMode() function call takes the number 8, and the string INPUT, and does work that we can't see to let us use the pin D8 as an input pin. You can use any number from 1 to 8 to choose D1 to D8 as the connector port, but we are going to use D8. Now, we can plug a button into that pin, and the board will read when we press the button. And lets do just that, plug a connector to a button into the D4 port. The button will not do anything yet, because the loop section is still empty, but its an important start. Do note the presence of a semicolon (;) at the end of the line of code, these are required at the end of every line of code that doesn't end with curly braces. If a semicolon is missing, the arduino IDE will give you a hard to read error message that generally means a semicolon was forgotten. 

Go ahead and add another pinMode() call to setup another digital port of your choice to be used for an output instead of an input, and then plug in the LED from the nightlight tutorial to that port. If you need to use an analog port in the future, to specify the analog ports, or A0, A1, A2, and A3 on the shield, we simply insert an A before the number we add into the pinMode call, and it looks like this:

>  pinMode(A0, ____);

### Main Loop
The main loop() function, shown below, repeatedly runs after setup() is complete until the power cable is unplugged or the machine turns off. This is where we will be inserting most of our own code, asside from defining certain pins to certain values. 

>  void loop() {
>    // put your main code here, to run repeatedly:
>
>  }

This is the section that you would put the bulk of the code you wanted to run. In the previous Nightlight tutorial, the code to read the light sensor, check for the button, and turn the light on are all in this section. For our program, we are just going to detect if the button is being pressed, and then turn on the LED if it is. In order to accomplish this, we will need to know the conditional if, and the functions to turn the LED on and off. 

The Galileo board handles the pins through the use of the digitalRead() and digitalWrite() functions. The digitalRead() function takes a digital port value, such as 1 through 8, as its one and only input value. the digitalWrite() function takes in two input values, and they are, in order, a digital port value, and a keyword such as HIGH, LOW, or NULL. DigitalWrite() sends an amount of power specified by the keyword to the digital port specified, with HIGH being the equivalent of On, and NULL being the equivalent of Off. 

>  digitalRead( 8 );          // reads in the state of the digital port 8
>
>  digitalWrite( 4, HIGH );   // sends a HIGH power signal to the digital port 4, turning it on

You might be thinking, what use is there in just reading in a value from the digital port? If you just read it in, it does nothing and the value is lost. Therefore we need to find a way to save that value in the code. This is where variables come into play. A variable is a single word that we can designate a value to. We can name these variables anything we want, as long as the names only have letters and numbers in them. The following is an example of a variable being declared of type of int, which only accepts integer numbers as its value.

>  int buttonInput;

This is added as one of the first lines in the main loop() to be used elsewhere in the program. Go ahead and add an integer variable to the loop, and name it whatever you want. Be sure to end the statement with a semicolon. When you want to use the variable elsewhere, you don't need to use int anymore, and you simply call the variable by its name, such as buttonInput. This variable is what we needed to catch the value of the button using digitalRead(). 

>  buttonInput = digitalRead( 8 );

A single equals sign is used to set the value of a variable to whatever value after the equals. We can add that line of code after the line with int buttonInput. IMPORTANT: You MUST declare a variable before you can use it anywhere else in the program, so always put the declarations towards the start of the main loop. 

Now that we have saved the state of the button, we need to find a way to use that information. This is where the if() statement comes in. An if() statement reads in an expression between the parenthesis, and then executes the next line of code if the expression is true. Otherwise, the code between the if's curly braces are ignored for that loop. An else statement can be added after the curly braces to provide an alternative section of code to run if the expression is not true, or false. 

>  if( buttonInput == 1 ) {
>
>    digitalWrite( 4, HIGH );
>
>  } else {
>
>    digitalWrite( 4, NULL );
>
>  }

That code will check if buttonInput, which reads whether the button is pressed, is equal to one. If it is, that means the buttonInput variable was set to 1 which is the value the button returns in digitalRead() when it is pressed. Notice the TWO equals signs, this is used to compare two values, and is resolved into a TRUE if the statement makes sense, or FALSE if it doesn't. When the button is pressed, this expression will evaluate to TRUE, and digitalWrite( 4, HIGH ) will run, which will turn the LED on. 

In the case that the buttonInput == 1 expression is FALSE, it will skip the code between the curly braces of the if, and if there is an else statement after the curly braces, it will then run the code of the else. So in this case, when the buttonInput is 0 from not being pressed, it will run the code digitalWrite( 4, NULL ), which will turn the LED off. 

Once we have added that conditional to the main loop of our program (make sure that the amount of left parenthesis and curl braces, and right parenethesis and curly braces are equal and in the right places), we are ready to finally run our program. Make sure the Galileo board is powered and plugged into the computer, and then press the Upload button to compile and send the program to our board. If all went well, then the program is sent to our board, and if we hook up the button and LED to the ports we chose earlier, the LED should turn on when we press the button, and turn off when we let go of the button. If not, then the IDE ran into a compile error and some red text has shown on the bottom of it. Try to figure out what went wrong from the error message, and if you can't figure it out, feel free to ask your peers or an aid for help. 

## Results
This tutorial will hopefully have taught you about some very basic elements of programming. Looking at past and future code will hopefully reinforce the ideas taught here, and let you more easily maneuvre through the code that we have written. There are several topics that we haven't covered because there  is more stuff than is possible to write in this tutorial, so if you ever have questions about what a bit of syntax means, simply ask an aid for help in clarifying what some piece of code means or why it is there. 

## Exploratory Questions

## We accomplished the following in this tutorial

  1. Discussed the basic structure of an Arduino program
  2. Learned how to declare and use variables of int type
  3. Briefly went over what a function is and how to use it
  4. Learned how to use if and else statements. 
