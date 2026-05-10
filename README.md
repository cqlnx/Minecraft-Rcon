# Minimal Minecraft RCON

A functional Minecraft RCON client for Python, designed to be as short as possible.

---

## The One-Liner

The core of this project is a functional client condensed into a single line of code. It handles the socket connection, authentication, and a command loop.
<details>
<summary>Click to view the code</summary>

```python
import socket,struct,random,getpass,sys as s;h,p=input("Host: "),int(input("Port: "));c=socket.socket();c.connect((h,p));pck=lambda t,b:struct.pack("<iii",8+len(b:=b.encode()+b"\0\0"),random.randint(1,2**31-1),t)+b;rec=lambda:(lambda n,d:(struct.unpack("<ii",d[:8])[0],d[8:-2]))((n:=struct.unpack("<i",c.recv(4))[0]),c.recv(n));c.sendall(pck(3,getpass.getpass()));i,_=rec();i==0 and (i:=rec()[0]);i==-1 and exit();[c.sendall(pck(2,k)) or print(rec()[1].decode(),end="") for k in iter(lambda:input("\n> "), "")]
```
</details>

---

## Features

- Zero Dependencies: Uses only standard Python libraries like socket and struct.
- Secure: Uses getpass so your password doesn't show up in the terminal while typing.
- Interactive: Includes a prompt loop to send multiple commands in one session.

---

## Usage
1. Enable RCON in your server.properties file.
2. Run the script: python rcon.py.
3. Enter your server details and password when prompted.

---

## Files

- rcon.py: The one-liner version.
- rconclean.py: The same logic but formatted for readability.
