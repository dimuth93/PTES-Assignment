
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

1.	Writing a C program with vulnerabilities
