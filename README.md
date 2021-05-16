# ABOUT
 This is a simply Python program that takes in a file with Pseudo assembly code and then outputs Verilog snippets that you can paste into your project.

# ISA
| Operation | Function | Instruction Encoding |
| --- | --- | --- |
| Load Rx, Data | Rx <- Data | 00,Rx,Data |
| Store Rx, Data | LEDs <- [Rx] | 01,Rx,XXXX |
| Move Rx, Ry | Rx <- [Ry] | 10,Rx,Ry,XX |
| Add Rx, Ry | Rx <- [Rx] + [Ry] | 11,Rx,Ry,00 |
| Sub Rx, Ry | Rx <- [Rx] - [Ry] | 11,Rx,Ry,01 |
| And Rx, Ry | Rx <- [Rx] & [Ry] | 11,Rx,Ry,10 |
| Not Rx | Rx <- ![Rx] | 11,Rx,XX,11 |

# USAGE
This program should work from the terminal with either python or python3 command. You may have to install Python if it is not already on the ECE drive.

The ```-i``` argument is required and tell it where the input file is. The ```-o``` argument tells it where to write the verilog code. If you don't specify a output file then it's just printed to the console.

 ```/home/ecestudent/compiler$ python3 simple_compiler.py -i prog1.txt```

 or

  ```/home/ecestudent/compiler$ python3 simple_compiler.py -i prog1.txt -o out.txt```

# EXAMPLE INPUT
	LOAD R0, 13
	LOAD R1, 1
	STORE R0
	ADD R0, R1
	LOAD R3, 12
	ADD R3, R0
	MOVE R2, R3

# EXAMPLE OUTPUT
	limit = 7;
	case(count)
			1: inst = 8'b00001101; // LOAD R0 13

			2: inst = 8'b00010001; // LOAD R1 1

			3: inst = 8'b01000000; // STORE R0

			4: inst = 8'b11000100; // ADD R0 R1

			5: inst = 8'b00111100; // LOAD R3 12

			6: inst = 8'b11110000; // ADD R3 R0

			7: inst = 8'b10101100; // MOVE R2 R3

			default: inst = 8'b00000000;
	endcase

# ERRORS
If you type a invalid instruction, a non-existant register, or a load number that is greater than 15 you will get an error message that will show where the error is.

	Invalid Register: Expected a load value from 0-15 but got ->: 20
	File prog1.txt, line 1

	LOAD R0, 20
			 ^^