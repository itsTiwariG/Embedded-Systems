Linker File -  
1. Linker Files -  
● These files specify the memory layout of the embedded system which includes 
the placement of the data sections, stack, heap and the other memory regions. 
● They are used with the compilers to generate the binary which is executable for 
the targeted microcontroller. 
2. Define the Memory regions -  
● The bootloader will be stored at the starting address of the flash which is 
0x8000000. The size of this memory region is kept to be 1Mb, we change 
the size of the memory according to the bootloader.

3. Assigning Sections to the Memory regions -  
● Use the keyword ‘SECTIONS’ which is used to assign the data and the code 
sections in the memory regions 
● Then mention the placement of the various sections within the memory regions 
with the help of the memory addresses.

4. Handling the stack and the heap - 
● To allocate the memory to the heap - ‘_heap’ and for the stack ‘_stack’ within the 
memory regions. Assign the size as well. 
5. Linking the external libraries and objects -  
● Use the directives such as ‘EXTERN’ or ‘INCLUDE’ and mention in the memory. 
Developing the Boot Code -  
1. Configuring Bootloader settings -  
● The FLASH_APP_ADDR in the bootloader code specifies the starting 
address of the application program, this is required as the bootloader needs to 
know where the application programs will starts and it will be loading application 
program from the specifies address. 
● Set up the memory mapping, in the linker script we had kept the size of 
bootloader’s region to be 1Megabits, adding 1Mb to 0x8000000, we get 
0x8100000. This is the address where our application programs will be stored. 

2. Implementing Bootloader logic -  
● Write the code to implement the bootloader. 
● The Jumpaddress specifies the address the we need to jump to in order to 
start executing our application program. 
● SCB->VTOR has been used to set the interrupt vector table for the 
application program which will be specified by the first four bytes of the 
location where application program is stored in our case it is 0x8100000 and 
interrupt vector table will be from 0x8100000 to 0x8100003. Without setting up 
the interrupt vector table our program might not work as interrupt handling for the 
application programs will be hindered. 
● The Jump_To_Application is a function pointer which will hold the starting 
address of the application program, which in our case is obtained by de
referencing the value store at 0x8100004. 
● Finally we call the Jump_to_application function in order to start executing the 
desired function.

1. Design the Application Architecture -  
● Plan the modules, layers and data flow diagrams. 
● Any configuration that needs to be made can be done by using the 
Bootloader.ioc file. 
2. Configuring Project Settings -  
● We need to configure the settings such as the target microcontroller and 
debugging settings. 
● Set the paths, library dependencies and build configs. 
3. Implementing Application Logic -  
● Write the code to implement the functionality based on the requirements, in our 
case we will just write a simple program to blink and LED.  
4. Application program linker script.  
● The flash region of the application program starts from 0x8100000, which is 
where the memory region of the bootloader ends, the size of the flash 
region is kept to be 32KiloBytes, after the end of the app region we have 
mymemory region which was created for the miscellaneous task.

Combining the Bootcode and Appcode  
1. The bootloader loads a very simple application program of blinking an LED, the 
application program can be any general application program but for simplicity we have 
just began with blinking an LED. 
2. Execute the application program along with the Boot Code 
● To do that, we will enter into the debug configuration. We will  go to the 
startup tab. Through there, we can add a different ELF (Executable and 
Linkable Format). We can load two or more ELFs at the same time. We select 
the application project over the debug one and just hit OK. So, we’re going to see 
that both will be presented. One is the main, and the other one is just part of the 
entire debug session.
