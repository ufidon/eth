# Programming for security professionals

Objectives
---
- Explain basic programming concepts
- Write a simple C program
- Explain how Web pages are created with HTML
- Describe and create basic Perl programs
- Explain basic object-oriented programming concepts

## C programming

Introduction to Computer Programming
---
- Computer programmers must understand the rules of programming languages
  - Programmers deal with syntax errors
- One minor mistake and the program will not run
  - Or worse, it will produce unpredictable results
- Being a good programmer takes time and patience


Computer Programming Fundamentals
---
- Fundamental concepts
  - Branching, Looping, and Testing (BLT)
  - Documentation
- Function
  - Mini program within a main program that carries out a task


Branching, Looping, and Testing (BLT)
---
- Branching
  - Takes you from one area of the program to another area
- Looping
  - Act of performing a task over and over
- Testing
  - Verifies some condition and returns true or false


A C Program
---

```c
// A simple C program
#include <stdio.h> // standard library for printf
int main(int argc, char* argv[]){ /* Every C program needs a main() */
  printf("Ethical hacking is fun!\n");

  return 0;
}
```

```c
// print command line parameters
#include <stdio.h> // standard library for printf
int main(int argc, char* argv[]){ /* Every C program needs a main() */
	int i;
  printf("the number of cmd parameters: %d\n", argc);
	
	for (i=0; i< argc; i++)
		printf("%d: %s\n", i, argv[i]);
	
  return 0;
}
```

```c
// find the area of a circle
#include <stdio.h> // standard library for printf
#include <stdlib.h>
int main(int argc, char* argv[]){ /* Every C program needs a main() */
	double radius;
	if( argc != 2){
		printf("usage: %s radius\n", argv[0]);
		return 1; 
	}
	
	radius = strtod(argv[1], 0);
	
	if (radius <= 0)
	{
		printf("The radius must be positive.\n");
		return 2;
	}
	
	
	 printf("the area of the circle with radius %g is %g \n", radius, 3.1415926*radius*radius);
	
	
  return 0;
}
```

- Filename ends in .c
- It's hard to read at first
- A single missing semicolon can ruin a program
- Comments make code easier to read


Branching and Testing
---

```c
#include <stdio.h> 
int main(int argc, char* argv[]){
  int age;
  printf("Enter your age: ");
  scanf("%d", &age);
  if(age >= 18)
    printf("You are eligible to take Ethical Hacking.\n");
  else
    printf("You are NOT eligible to take Ethical Hacking.\n");

  return 0;
}
```


Looping
---

```c
#include <stdio.h> 
int main(int argc, char* argv[]){
  int i;

  for(i=0; i<10; i++)
    printf("I will practice Ethical Hacking...\n");

  return 0;
}
```


Branching, Looping, and Testing (BLT)
---
- Algorithm
  - Defines steps for performing a task
  - Keep it as simple as possible
- Bug
  - An error that causes unpredictable results
- Pseudocode
  - Natural language used to create the structure of a program


Pseudocode For Port Scanning
---
- while(there are ports left)
  - take a port
  - care out port scanning


Documentation
---
- Documenting your work is essential
  - Add comments to your programs
  - Comments should explain what you are doing
- Many programmers find it time consuming and tedious
- Helps others understand your work


Bugs
---
- Industry standard
  - 20 to 30 bugs for every 1000 lines of code
- Windows 2000 contains almost 50 million lines
  - And fewer than 60,000 bugs (about 1 per 1000 lines)
- Linux has 0.17 bugs per 1000 lines of code


Learning the C Language
---
- Powerful and concise language
- UNIX was first written in assembly language and later rewritten in C
- C++ is an enhancement of the C language
- C is powerful but dangerous
  - Bugs can crash computers, and it's easy to leave security holes in the code


Assembly Language
---
- The binary language hard-wired into the processor is machine language
- Assembly Language uses a combination of hexadecimal numbers and expressions
  - Very powerful but hard to use


Compiling C in Ubuntu Linux
---
- Compiler
  - Converts a text-based program (source code) into executable or binary code
- To prepare Ubuntu Linux for C programming, use this command:
  ```bash
  sudo apt-get install build-essential 
  ```
- Then you compile a file named "eth.c" with this command:
  ```bash
  gcc eth.c –o eth
  ```


Include and Function
---
- #include statement
  - Loads libraries that hold the commands and functions used in your program
- A Function Name is always followed by parentheses ( )
  - Curly Braces { } shows where a function begins and ends
- main() function
  - Every C program requires a main() function
  - main() is where processing starts
- Functions can call other functions
  - Parameters or arguments are optional


Declaring Variables
---
- A variable represents a numeric or string value
- You must declare a variable before using it


Variable Types in C
---
- char, short, int, long, long long
- float, double
- string


C Operators
---
- Mathematical operators
  - unary: +, -, ++, --
  - binary: +, -, *, /, %
- Logical operators
  - ==, !=, >, <, >=, <=
  - &&, ||, !


Practice ✏️ 
---
- Buffer Overflow
```c
#include <stdio.h> 
int main(int argc, char* argv[]){
  char name[10];
  printf("Enter your name? ");
  scanf("%s", name);
  printf("Hello, %s\n", name);

  return 0;
}
```


Buffer Overflow Defenses
---
- Address space layout randomization (ASLR) 
- Data execution prevention
- Detecting stack smashing with a canary value


## Web programming

Understanding HTML Basics
---
- HTML is a language used to create Web pages
- HTML files are text files
- Security professionals often need to examine Web pages
  - Be able to recognize when something looks suspicious


Creating a Web Page Using HTML
---
- Create HTML Web page in text editors
- View HTML Web page in a Web browser
- HTML does not use branching, looping, or testing
- HTML is a static formatting language
  - Rather than a programming language
- < and > symbols denote HTML tags
  - Each tag has a matching closing tag
  - \<HTML\> and \</HTML\>


HTML formatting tags
---
- \<H1\>, \<H2\>, \<H3\>, \<H4\>, \<H5\> and \<H6\>.
- \<P\>, \<BR\>
- \<B\>, \<I\>


## Scripting

Understanding Practical Extraction and Report Language (Perl)
---
- PERL 
  - Powerful scripting language
  - Used to write scripts and programs for security professionals


Background on Perl
---
- Developed by Larry Wall in 1987
- Can run on almost any platform
  - *NIX-base OSs already have Perl installed
- Perl syntax is similar to C
- Hackers use Perl to write malware
- Security professionals use Perl to perform repetitive tasks and conduct security monitoring


Understanding the Basics of Perl
---
- find the usage of perl
  ```bash
  perl -h
  ```
- printf format, identical to C printf


Understanding the BLT of Perl
---
- Some syntax rules
  - Keyword “sub” is used in front of function names
  - Variables begin with the $ character
  - Comment lines begin with the # character
  - The & character is used when calling a function
```perl
#/usr/bin/env perl

$word = "Hack";
&speak;

$word = "or";
&speak;

$word = "die!";
&speak;

sub speak{
  print "$word\n";
}

# do a ping sweep
for ($p=1; $p<100; $p++){
  print qx"ping 10.0.2.$a -c 2 -w1";
}
```


Branching in Perl
---
```perl
#/usr/bin/env perl
print "Enter your IQ (1-10): ";
open (INFO, "-");
$IQ = <INFO>;
if ($IQ > 7){
	print "eligible!\n";
} else {
	print "illegible!\n";
}

```


## Object-Oriented Programming (OOP)

Understanding Object-Oriented Programming Concepts
---
- New programming paradigm
- There are several languages that support object-oriented programming
  - C++
  - C#
  - Java
  - Perl 6.0
  - Object Cobol


Components of Object-Oriented Programming
---
- Classes
  - Structures that hold pieces of data and functions
- The :: symbol
  - Used to separate the name of a class from a member function
  - Example:
    - ClassName::method()


An example class in C++
---
```c++
class HackingTool
{
public:
	char name[50];
	char description[200];
	char introdate[20];

	bool hack(char ip[])
	{
		// perform hacking on ip
	}
};
```


Ruby
---
- [Metasploit is written in Ruby](https://github.com/rapid7/metasploit-framework)


[Esoteric programming languages](https://esolangs.org/wiki/Main_Page)
---
- [lolcode](http://www.lolcode.org/) 
- [brainfuck](https://esolangs.org/wiki/Brainfuck)


# References
- [How do I call Windows DLL functions from Ruby?](https://stackoverflow.com/questions/1025086/how-do-i-call-windows-dll-functions-from-ruby)