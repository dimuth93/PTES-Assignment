
# 1.Introduction

## 1.1	What is buffer overflow?

A buffer is a sequential memory segment that includes anything from a character string to an integer sequence. When more data is put inside a fixed buffer than the buffer can manage, a buffer overflow or buffer overrun occurs. The additional information, which needs to go anywhere, can overwriting or corrupting the data held in the space into the adjacent memory area. This overflow normally leads to a system crash, but it often gives an attacker a chance to execute arbitrary code or to handle code error in order to cause malicious actions.

Many languages are vulnerable to buffer overflow attacks. However, depending on the language that the vulnerable program write, the extent of such attacks varies. In Perl and JavaScript, for example, code is typically not prone to buffer overflows. Nevertheless, an attacker may be able to fully compromise a targeted framework through a buffer overflow in a program written in C++ , C, Fortran or Assembly.

Cybercriminals use buffer overflow problems to alter the application's execution direction by overwriting portions of the program. The extra malicious data may contain code designed to trigger specific actions — in effect, the attacked application may receive new instructions that might lead to unauthorized system access. Hacker techniques that use the weakness of buffer overflow differ by architecture and operating system.


## 1.2	Where is the vulnerability?

The first Internet worm (Morris internet worm), which migrated from system to system about 30 years ago (1988-11-02), used gets() and buffer overflow. The main issue is that the function does not know the buffer size and so continues to read until a newline is found or when an EOF is found, and the buffer boundaries it was provided may overflow.

 - gets()
 
The fgets) (function reads and stores them in string at most less than the number of characters specified by size of the stream. Reading stops at the end-of-file or error when a newline character is detected. The newline is kept, if necessary. A '\0' character is annexed to end the string if any characters are read and there is no mistake.

The function gets( ) except that the newline character (if any) is not saved in the string, is identical to fgets() ,with infinite size and a stdin stream. It is the duty of the caller to ensure, if any, that the input line is short enough to suit the string. Unable to safely use the gets() feature. The use of the features enables malicious users to alter arbitrarily the functionality of a running program with a buffer overflow attack, due to its absence of checks of limits and the failure of the calling system.

- strcpy() & stpcpy()

Copy the source string to destination (including the '\0' terminal) in stpcpy() and strcpy() functions, stpncpy() and strncpy() functions are copied from source to destination in the majority of LEN characters. The remainder of destination is loaded with '\0' characters if it is less than LEN  characters. Destination is not finished otherwise. The source and goal strings should not be overlapping because the action is unknown.

Strcpy() is easily misused and malicious users can arbitrarily alter the functionality of a running program by means of a buffer overflow assault.

- strcat() and strcmp()

The function strcat() can be easily misused so that malicious users may alter the configuration of a running program arbitrarily through a buffer overflow assault. No strcat() should be used. Instead, use strncat() or strlcat() to ensure that no more than it can carry characters are copied to the destination buffer. Note that it can also be difficult to strncat(). It may be a security problem to truncate a number. Since the truncated string is not as long as the original, the truncated resource can refer to a completely different resource and can lead to very misconformity.

- sprintf()

The sprintf() and vsprintf() functions are easily abused to allow malicious users to modify the functionality of an executed program in a buffer overflow attack arbitrarily. Since sprintf() and vsprintf() presume an infinite string, callers must make sure the actual space is not covered; sometimes this is difficult to ensure. The snprintf() interface should instead be used by programmers for stability.

- printf() and Uncontrolled format string

A malicious user may print data from the call stack or maybe other positions on the memory using the '% 'and '%x' formats tokes, among other items. Arbitrary data may also be written to arbitrary locations using the%n token, with printf() commands and similar functions for writing the number of bytes formatted to the stack address.



## 1.3	Impact of this vulnerability?

This issue can be expressed in many ways:

1. No visible effect of any sort

2. Immediate end of system (crash)

3. Late termination (1 second later, maybe 15 days later) in the lifespan of the program

4. Closure of an unrelated plan
	
5. False program conduct and/or calculation


<br/><br/>

# 2.Mitigation

## 2.1	How to mitigate these vulnerabilities?


- fgets() and gets_s()

The function fgets() has similar behavior to gets() and is defined in C99. Two more arguments are taken from the fgets() function: the number of characters to be read and an input source. Specifying stdin as stream allows fget() to simulate gets()'s behaviour.

- strcpy s() and strcat s()

The functions strcpy s() nd strcat s() is defined as near substitutions for strcpy() and strcat() in ISO / IEC TR 24731. These functions have an additional rsize t argument, which determines the maximum buffer capacity.

- strncpy s() and strncat s()

The functions strncpy s() and strncat s() which are closely substituted for strncpy() and strncat() are specified by ISO / IEC TR 24731.This function copies a number of successive characters from a source string to a destination character list, not more than a specified number (characters that follow a null character are not copied). If no null character has been copied, a null character is specified for the last character of the target character sequence.

<br/><br/>

# 3.CVS Details

**CVE-2005-0753**

Analysis Description
Buffer overflow in CVS before 1.11.20 allows remote attackers to execute arbitrary code.

## 3.1 Arbitrary code

Arbitrary code means malicious software code that the hacker writes and typically does wrong. This can open a back door in a computer network, steal sensitive data or throw out safety measures (such as passwords), or make the machine a zombie to launch attacks on other computers. And finally, the arbitrary execution of code means that somehow, by exploiting a bug, the bad actor will upload the malicious code to a remote computer and manipulate the remote computer to execute, or run, the code. The hacker is said to have created an execution of arbitrary code.

It is highly sophisticated to upload malicious code to the remote computer, also called injection. The hacker can overwrite portions of the file in memory of the original program. The malware can be sneaked into buffers or caches by using defections on operating systems or even microprocessors and the bad program will then automatically run.

<br/><br/>
# 4.Exploitation

1. Write a C program with vulnerabilities

![image](https://user-images.githubusercontent.com/31270985/82113310-b65f8280-9772-11ea-8775-25b673d6f4d9.png)
<br/><br/>

2. Compile the code and create an executable file 

“-fno-stack-protector” : Disables stack protection.
You can see some warnings about gets() function, while compiling the code.

<br/>
![image](https://user-images.githubusercontent.com/31270985/82113327-d131f700-9772-11ea-9de9-2aba2fd6ce26.png)
<br/><br/>


3. Start ‘socat’ and start listening to a PORT

![image](https://user-images.githubusercontent.com/31270985/82113335-e27b0380-9772-11ea-922d-adb26270a12e.png)
<br/><br/>

4. Connect to the PORT using ‘netcat’ and try out your code first.

![image](https://user-images.githubusercontent.com/31270985/82113344-fb83b480-9772-11ea-93e0-5b74f7a4b35a.png)
<br/><br/>

5. Start developing a Socket using python code, which connects to your localhost (This can be either localhost IP or your target’s IP). As I have connect to the PORT using localhost, I am using localhost IP here.

![image](https://user-images.githubusercontent.com/31270985/82113366-20782780-9773-11ea-81d5-86a820021b00.png)
<br/><br/>

6. Tryout “Format String Vulnerability” using special characters. I am using some “%p” to leak some memory addresses.

![image](https://user-images.githubusercontent.com/31270985/82113377-38e84200-9773-11ea-89b5-021e33d94670.png)
<br/><br/>

7. To check these memory addresses, we need to look the memory map of your program and find out the stack address.

‘ps aux | grep caf’ : Sort the process list attached
‘sudo cat /proc/pid/maps’ : To access the memory map
<br/>

![image](https://user-images.githubusercontent.com/31270985/82113397-5ae1c480-9773-11ea-8d89-7dc11d75c08a.png)
<br/><br/>

8. Attach GDB to your process and try to find out any details from stack memory address

I am using x/16gx here to look for “16 giant words”<br/>

![image](https://user-images.githubusercontent.com/31270985/82113413-806ece00-9773-11ea-8c71-9580828ca54d.png)
<br/><br/>

9. Disassemble your main function and set a break pointer at return pointer

![image](https://user-images.githubusercontent.com/31270985/82113430-a1372380-9773-11ea-901e-746710e9fbab.png)
<br/><br/>

10. Try some identifiable characters with “%p” and try to identify them using GDB. (Watch the change in stack memory address)

Even though you might not see it the memory address itself. Try to go back few characters and try it again.<br/>

![image](https://user-images.githubusercontent.com/31270985/82113443-c4fa6980-9773-11ea-8006-31a9158a608e.png)
<br/><br/>

11. Then use some “%p,%p,%p” (8 characters) as input and attach GDB. Go back 9 characters and print them as string and see.

![image](https://user-images.githubusercontent.com/31270985/82113462-e9564600-9773-11ea-9130-8468f344f5b5.png)
<br/><br/>

12. In your python program, send some “%p,%p,%p” to your socket and retrieve the response. 

You might have to separate string stream using ‘commas’. Print the 2nd value using ‘[1]’ and convert it to Base16 and also subtract 9. And also sometimes you have to add some loop around, because the receiving is so fast that server won’t be able to response it.<br/>

![image](https://user-images.githubusercontent.com/31270985/82113478-0723ab00-9774-11ea-9295-3508f7799a27.png)
<br/><br/>

13. Then generate some long random non-repeatable string stream and paste it in the program input to have a buffer overflow. Then look at the stack and find the offset.

![image](https://user-images.githubusercontent.com/31270985/82113538-62ee3400-9774-11ea-89de-26001e57819a.png)
<br/><br/>

14. Copy some of the string value, and delete the rest of it starting from the search value to end. Assign “padding” variable to it.

Padding: This much of content needs to overwrite the return pointer.
<br/>

![image](https://user-images.githubusercontent.com/31270985/82113549-700b2300-9774-11ea-9333-a2168e53bb65.png)
<br/><br/>

15. Start designing the payload.

Padding=Content needed to overwrite the return pointer
RIP= Integer value used to point out the shellcode
“x\90”*64 = some ASCII escape characters
Shellcode=A code developed by hackers to run a program
<br/>

![image](https://user-images.githubusercontent.com/31270985/82113565-87e2a700-9774-11ea-8caa-5589d480960d.png)
<br/>

29 byte shellcode I used to execute “/bin//sh”
![image](https://user-images.githubusercontent.com/31270985/82113571-9f219480-9774-11ea-918f-44bee89ec1ba.png)
<br/><br/>

16. Apply your shellcode to your coding and start the program. You’ll the ‘Your program is now executing a different program” message, which occurred due to your shellcode. It’ll give ‘root’ access in your targeted Linux pc.

In additionally you can use python ‘telnet’ library to keep and maintain the session.
<br/>

![image](https://user-images.githubusercontent.com/31270985/82113595-d3955080-9774-11ea-965c-2980b66e9e67.png)
<br/><br/>

17. Results

![image](https://user-images.githubusercontent.com/31270985/82113599-dee87c00-9774-11ea-9f3a-67d8a88ee786.png)
<br/>
![image](https://user-images.githubusercontent.com/31270985/82113603-e740b700-9774-11ea-8294-3f1b4b580970.png)
<br/><br/>

# REFERENCES


