Introduction 
Mastermind is a popular code-breaker game that is played with two players.  The puzzle is made up of four pegs which get slotted with colored pieces. One player sets the puzzle's answer that the other player tries guess. With each move played, the player's move is scored against the puzzle answer. Each piece is scored as either being in the right place in the answer, in the answer but currently in the wrong place, or not in the answer at all.  If you are unfamiliar with Mastermind, please use the link to review the rules of the game where you can also play for funLinks to an external site. to get some practice with the game. 

This game has a very rich computer history.  The game is based on an older, paper based game called Bulls and Cows. A computer adaptation of it was run in the 1960s on Cambridge University’s Titan computer system written by Frank King, where it was called 'MOO'. Other versions were created on very early computers using the TSS/8 time sharing system and for the Multics system running at MIT. The game strategy has also been widely studied. In 1977, Donald Knuth, a famous Computer Scientist at Stanford University, demonstrated that, with six colors and four spots, the codebreaker puzzle can solved the pattern in five moves or fewer, using an algorithm that progressively reduces the number of remaining possible patterns.

For our purposes, the skeleton game I am giving you will use six colors and four spots and, just to be a bit challenging, will need to be solved in four moves or fewer.
Your task

Your assignment is to complete this C++ program skeleton (XCodeLinks to an external site. VS2022Links to an external site.) to produce a program that implements the described behavior. (We've indicated where you have work to do by comments containing the text TODO.  Please remove those comments as you finish each thing you have to do.)  The program skeleton you are to flesh out provides alot of code but you will be focusing your attention on the classes: Piece, Move, Score, Board and Mastermind.  You will need to complete code for the Move, Score, Board and Mastermind classes.  Details of the interface to all of these classes are in the program skeleton, but here are the essential responsibilities of each class:  

In order to understand how the skeleton works, let's look at the COLOR enumeration and the class Piece.  The COLOR enumeration is defined in the file Enums.h and is shown below:

image.png


This enumeration defines a value for every available color plus another value for any invalid value that might be entered.  This enumeration is fully defined and needs no changes to be made by students.

The Piece class represents a single played spot in one round of play in the Mastermind game.  Please note the class diagram shown below:

image.png


The constructor of this Piece class enables client code to create a Piece from a single character or from the first letter of a string.  By default, the Piece will have an NOTVALID COLOR value.  Once defined, this class enables client code to access the underlying COLOR or convert that single COLOR value into a matching string representation.  This class is fully defined and needs no changes to be made by students.  If you scroll down, you will find driver code I have supplied in the assignment instructions that show you how you can work with objects of the Piece class.

An ordered collection of four pieces played in a single round of play in the Mastermind game is represented by the class Move.  A Move is made up of a set of four Pieces, as documented in the UML diagram shown below:

Move Class Relationships

image.png
Please note the class diagram shown below:

Move Class Diagram

image.png
Each Move holds an array of Pieces.  The length of the array is controlled by the constant REQUIREDLENGTH which is defined in the file Settings.h.  By default, each Piece will be NOTVALID.  Client code uses the operation setPiece( ... ) to specify a single piece of a Move object.  The parameter i should be an index value into the array of Pieces between 0 and REQUIREDLENGTH - 1.  If the parameter i is out of bounds, setPiece will throw a std::logic_error back at the calling code, rather than offset outside the valid bounds of the array.  Similarly, the operation getPiece( ... ) allows client code to access one individual Piece of this move.   The parameter i should be an index value into the array of Pieces between 0 and REQUIREDLENGTH - 1.  If the parameter i is out of bounds, getPiece will throw a std::logic_error back at the calling code, rather than offset outside the valid bounds of the array.   The operation to_string( ) returns the four colors that make up this Move as a string of four characters.  NOTVALID Pieces will be returned as the space character.   The operation setPieces( ... ) needs to be completed by CS students.  This operation should accept a four-character string and set each Piece of this Move object to the associated COLOR provided in the string parameter.  If the string parameter is not four letters long, this operation should throw a std::logic_error back at the calling code.  Please see the TODO comments in the class for further information.  If you scroll down, you will find driver code I have supplied in the assignment instructions that show you how you can work with objects of the Move class.

Each round of play in the Mastermind game needs to be scored, color-by-color, against the correct answer of the game.  This scoring gets performed by the class Score which works with the enumeration ANSWER.  The ANSWER enumeration is defined in the file Enums.h and is shown below:

Answer enumeration

image.png
Once scored, each Piece in a Move will either be RIGHT, WRONG or MAYBE.  RIGHT means that exact color is in the same matching place when comparing the Score's Move to the correct answer.  WRONG means that exact color has no place in the correct answer when comparing the Score's Move to the correct answer.  MAYBE means that exact color is found in the correct answer but is currently located in the wrong position of the Score's Move.

Each Score holds an array of ANSWER.  The length of the array is controlled by the constant REQUIREDLENGTH which is defined in the file Settings.h.  Please note the class diagram shown below:
By default, each ANSWER value will be WRONG.  But if supplied two Moves, one for the played word and one for the correct answer, a Score constructor should properly define each ANSWER value accordingly.  This second constructor needs to be completed by students.  Please see the TODO comments in the class for further information.  Client code uses the operation getAnswer( ... ) to access an individual ANSWER value for the index parameter i.  The parameter i should be an index value into the array of ANSWER between 0 and REQUIREDLENGTH - 1.  If the parameter i is out of bounds, getAnswer( ... ) will throw a std::logic_error back at the calling code, rather than offset outside the valid bounds of the array.  A Score object can be converted into a string by calling to_string( ).  RIGHT answers will be printed as an 'R', WRONG answers will be printed as a '_' and MAYBE answers will be printed as an 'M'.  This operation isExactMatch( ) needs to be completed by students.  It should return true when the ANSWER array holds all RIGHT values.  Please see the TODO comments in the class for further information. If you scroll down, you will find driver code I have supplied in the assignment instructions that show you how you can work with objects of the Score class.

To help you understand the positional scoring, please consider the following examples:

Move move	Move answer	Score( move, answer ).to_string( )	Score( move, answer ).isExactMatch
"GGPP"	"GGPP"	"RRRR"	true
"GPOB"	"GOPB"	"RMMR"	false
"GGOP"	"OPGG"	"MMMM"	false
"GGOP"	"BYBY"	"____"	false
"GGOP"	"OPGY"	"M_MM"	false
"GGOP"	"POGB"	"M_MM"	false
"GGYY"	"YBGB"	"M_M_"	false
"GGGY"	"YGGB"	"_RRM"	false
 

The class Board is repetitively called to print out the state of the Mastermind game in a string table shown with the end of each round of play.  Each Board is made up of a set of Moves and Scores, as documented in the UML diagram shown below:

Board UML Diagram

image.png
The length of the arrays of Score and Move is controlled by the constant TOTALROUNDSALLOWED which is defined in the file Settings.h.  Please note the class diagram shown below:

Board Class Diagram

image.png
Each Board is tracking the current round and provides a trivial accessor for that member value.  A Move and Score gets supplied to the Board with calls to endRound( ... ) which should

copy the two parameters into array data members at the index of the current round and
then increment the current round value. 
Accessors are available to retrieve a Move or Score.  In each case, the parameter round should be an index value into the array of Move or Score between 0 and TOTALROUNDSALLOWED - 1.  If the parameter round is out of bounds, these two getters should throw a std::logic_error back at the calling code, rather than offset outside the valid bounds of the array.  Please see the TODO comments in the class for further information.  If you scroll down, you will find driver code I have supplied in the assignment instructions that show you how you can work with objects of the Board class.

The Mastermind class plays the game with code found in main.cpp.  At all times, the state of the game will be one of the possible outcomes defined in the enumeration GAMEOUTCOME.  The GAMEOUTCOME enumeration is defined in the file Enums.h and is shown below:

GameOutcome Enumeration

image.png
The Mastermind class manages a Board, a winning Move with the correct answer as well as the current Move just recently played, as shown below:

Mastermind Aggregation Diagram

image.png
The class Mastermind is used in main.cpp to run the overall game.  If you scroll down, you will find driver code I have supplied in the assignment instructions that show you how you can work with objects of the Mastermind class.  Please note the class diagram shown below:

image.png
Mastermind Class Diagram

 Students need to complete determineGameOutcome( ).  Based on the state of the Board, this operation should return the proper GAMEOUTCOME value.  In addition, CS 31 Students need to complete endRound( ... ).  Based on the Move parameter, this operation should create a Score object, increment the round counter and supply this Score to this game's Board, saving this Score as the current score value and returning it back to the calling code.  Please see the TODO comments in the class for further information. 

You are free to create additional public and private methods and data members as you see fit.  However, the test cases will only be driving the public methods of the classes provided in the skeleton code originally.

The source files you turn in will be these classes and a main routine. You can have the main routine do whatever you want, because we will rename it to something harmless, never call it, and append our own main routine to your file. Our main routine will thoroughly test your functions. You'll probably want your main routine to do the same. If you wish, you may write functions in addition to those required here. We will not directly call any such additional functions. If you wish, your implementation of a function required here may call other functions required here.

The program you turn in must build successfully, and during execution, no method may read anything from cin. If you want to print things out for debugging purposes, write to cerr instead of cout. When we test your program, we will cause everything written to cerr to be discarded instead — we will never see that output, so you may leave those debugging output statements in your program if you wish.

CODEBOARD

Additionally, I have created a testing tool called CodeBoard to help you check your code.  CodeBoard enables you to be sure you are naming things correctly by running a small number of tests against your code.  Passing CodeBoard tests is not sufficient testing so please do additional testing yourself.  To access CodeBoard for Project 7, please click this link: https://codeboard.io/projects/161028Links to an external site..  I have pre-loaded this CodeBoard project with the Project 7 Skeleton code.  Inside the files named Move.h, Move.cpp, Board.h and Board.cpp, Score.h and Score.cpp, and Mastermind.h and Mastermind.cpp, copy and paste the versions you have developed.  CodeBoard uses its own main( ) to run tests against your code so you won't get any opportunity to provide a main( ) function.  Click Compile and Run.  However please be aware that no editing changes can be saved inside CodeBoard.  In this anonymous user configuration, CodeBoard is read-only and does not allow for saving changes.

In an effort to assist CS 31 students with the contents of your .zip file archive, H has created a Zip File Checker which will echo back to you the contents of your .zip file.  Please use this file checker to ensure you have named all your files correctly.

Programming Guidelines
Your program must not use any function templates from the algorithms portion of the Standard C++ library. If you don't know what the previous sentence is talking about, you have nothing to worry about. If you do know, and you violate this requirement, you will be required to take an oral examination to test your understanding of the concepts and architecture of the STL.

Your implementations must not use any global variables whose values may be changed during execution.

Your program must build successfully under both Visual C++ and either clang++ or g++.

The correctness of your program must not depend on undefined program behavior. 

What you will turn in for this assignment is a zip file containing the following 22 16 files and nothing more:

The files named Piece.h, Piece.cpp, Enums.h, Random.h, Random.cpp, Settings.h, which are part of the supplied skeleton and do not need to be changed at all as well as the files named  Board.h  and Board.cpp  that implement the Board class diagrammed above, the files  named  Move.h  and  Move.cpp  that implement the Move class diagrammed above, the files named Score.h  and  Score.cpp that implement the Score class diagrammed above, the files  named  Mastermind.h  and  Mastermind.cpp  that implement the Mastermind class diagrammed above and the file named main.cpp which will hold your main program. Your source code should have helpful comments that explain any non-obvious code.
A file named report.doc or report.docx (in Microsoft Word format) or report.txt (an ordinary text file) :
A brief description of notable obstacles you overcame.
A list of the test data that could be used to thoroughly test your functions, along with the reason for each test. You must note which test cases your program does not handle correctly. (This could happen if you didn't have time to write a complete solution, or if you ran out of time while still debugging a supposedly complete solution.) Notice that most of this portion of your report can be written just after you read the requirements in this specification, before you even start designing your program.
How nice! Your report this time doesn't have to contain any design documentation.


As with Project 3 and 4 and 5, a nice way to test your functions is to use the assert facility from the standard library. As an example, here's a very incomplete set of tests for Project 7.  Again, please build your solution incrementally.  So I wouldn't run all these tests from the start because many of them will fail until you have all your code working.  But I hope this gives you some ideas....  There are many others in CodeBoard for you to exercise your code on.

    #include <iostream>                        
    #include <string>
    #include <cassert>
    #include "Mastermind.h"
    #include "Score.h"
    #include "Move.h"
    #include "Board.h"
    #include "Piece.h"

    int main()
    {
           using namespace std;
           using namespace cs31;

           // test code
           Piece p;
           assert( p.getColor() == NOTVALID );
           p = Piece( "R" );
           assert( p.getColor() == RED );
           assert( p.getColorAsString() == "R" );

           Move m;
           p = m.getPiece( 0 );
           assert( p.getColor() == NOTVALID );
           m.setPieces( "RBRB" );
           p = m.getPiece( 2 );
           assert( p.getColor() == RED );
           m.setPiece( 2, 'y' );
           p = m.getPiece( 2 );
           assert( p.getColor() == YELLOW );

           Score s;
           assert( s.isExactMatch()  == false );
           assert( s.getAnswer( 2 ) == WRONG );
           m.setPieces( "RBRB" );
           Move theAnswer;
           theAnswer.setPieces( "YOYO" );
           s = Score( m, theAnswer );
           assert( s.isExactMatch() == false );
           assert( s.to_string() == "____" );
           theAnswer.setPieces( "rbrb" );
           s = Score( m, theAnswer );
           assert( s.isExactMatch() == true );
           assert( s.to_string() == "RRRR" );

           Board b;
           assert( b.getCurrentRound() == 0 );
           m.setPieces( "POPO" );
           theAnswer.setPieces( "YYOP" );
           s = Score( m, theAnswer );
           b.endRound( m, s );
           assert( b.getCurrentRound() == 1 );
           assert( b.getMoveForRound( 0 ).to_string() == "POPO" );
           assert( b.getScoreForRound( 0 ).to_string() == "MM__" );

           Mastermind game( "rbyo" );
           assert( game.answer() == "RBYO" );
           assert( game.gameIsOver() == false );
           m = game.play( "BBBB" );
           s = game.endRound( m );
           assert( s.to_string() == "_R__" );

           cout << "all tests passed!" << endl;
           return( 0 );
       }  
