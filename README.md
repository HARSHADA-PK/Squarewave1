Square Wave Generation using 8051 assembly code (Timer 0 Mode 1)

AIM:

To write an assembly language program to generate a square wave on Port 1 of the 8051 microcontroller using Timer 0 in Mode 1 (16-bit timer mode).

ALGORITHM:

1.Start the program.

2.Initialize Timer 0 in Mode 1 by loading #01H into the TMOD register.

3.Set up an infinite loop labeled AGAIN to continuously generate the square wave.

4.Send HIGH output to Port 1 (MOV P1, #0FFH) to generate the HIGH part of the waveform.

5.Call the DELAY subroutine to maintain the ON time of the waveform.

6.Send LOW output to Port 1 (MOV P1, #00H) to generate the LOW part of the waveform.

7.Call the DELAY subroutine again to maintain the OFF time of the waveform.

8.Repeat the process indefinitely using SJMP AGAIN for continuous square wave output.

9.In the DELAY subroutine:

     Load initial values into TH0 and TL0 registers.

10.Start Timer 0 using SETB TR0.

11.Wait until TF0 (Timer Flag 0) becomes 1.

12.Stop and clear Timer 0 and TF0 flag.

13.Return to the main program.

14.End the program with END.

PROGRAM:
```
ORG 0000H         

MOV TMOD, #01H    

AGAIN: 
    MOV P1, #0FFH  
    CALL DELAY      
    MOV P1, #00H    
    CALL DELAY      
    SJMP AGAIN      


DELAY: 
    MOV TH0, #0FFH
MOV TL0, #0FAH
    SETB TR0       
WAIT: 
    JNB TF0, WAIT  
    CLR TR0      
    CLR TF0      
    RET           


END
```
OUTPUT:
![WhatsApp Image 2025-10-18 at 12 44 54_4e6143ca](https://github.com/user-attachments/assets/d75ae235-a390-4e7b-b30e-449a609c1b6b)

Result:

The program was successfully executed in the Keil µVision simulator, and a square wave was generated at Port 1 of the 8051 microcontroller.




Program to Generate a Square Wave using 8051 Microcontroller C program

Aim:

To write an embedded C program to generate a square wave on Port 1 of the 8051 microcontroller using Timer 0 in Mode 1 (16-bit timer mode).

Algorithm:

1.Start the program.

2.Include the header file <reg51.h> for 8051 register definitions.

3.Initialize Timer 0 in Mode 1 by loading 0x01 into the TMOD register.

4.Enter an infinite loop using while(1) to continuously generate the waveform.

5.Set Port 1 HIGH (P1 = 0xFF) to produce the HIGH part of the square wave.

6.Call the delay function to maintain the ON period.

7.Set Port 1 LOW (P1 = 0x00) to produce the LOW part of the square wave.

8.Call the delay function again to maintain the OFF period.

9.In the delay() function:

      Load initial values into TH0 and TL0 registers.

10.Start the timer by setting TR0 = 1.

11.Wait until TF0 (Timer Flag 0) becomes 1.

12.Stop the timer and clear TF0 for the next cycle.

13.Repeat the above steps to generate a continuous square wave.

PROGRAM:
```
#include <reg51.h>  
void delay(void);  
void main(void)
{
    TMOD = 0x01;  
    while(1)
    {
        P1 = 0xFF;  
        delay();   
        P1 = 0x00;  
        delay();
    }
}
void delay(void)
{
    TH0 = 0xFF;    
    TL0 = 0xFA;     
    TR0 = 1;       
    while (TF0 == 0);  
    TR0 = 0;        
    TF0 = 0;        
}
```
OUTPUT:
![WhatsApp Image 2025-10-18 at 12 54 13_dcf57ab5](https://github.com/user-attachments/assets/fb3d8b21-87f2-4c10-bd7f-3cf288db7933)


Result:

The program was successfully executed using the Keil µVision simulator.
A square wave output was observed at Port 1, alternating between HIGH (5V) and LOW (0V) levels at equal intervals, confirming successful waveform generation.

