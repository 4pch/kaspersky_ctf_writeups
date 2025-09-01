# Writeup 1

Weak C2:
inside pcap has communication http between client and server, in cookies in client and server will have encrypted http communication.
In handshake:
client send:
{"method": "DH64", "p": "0xfdfcbe37cdd61355", "g": "0x2", "client_pub": "0x88bd8839e635f885", "iv": "5e48ac2731dae9521bdf50283430098c"}
server respond:
{"server_pub": "0x7ddb8841ffcfa8ff"}
after this is diffie hellman communication, my teammate is good in crypto and get:
client_priv = 0x92568a9e41dc9e4b
server_priv = 0x7f713232eb859a14
shared_secret = 0x8ced982cca3a22d7
after this communication is enable to view, one of the responses server will send a zip, the password is cracked by johntheripper and zip2john, and after cracking inside has a markdown file that have the flag (other communication have a email with other password, but is fake)

# Writeup 2

use of discrete_log from sage to bruteforce dh64 key
from there just GPT to the flag, all the c2 comns is in the session cookies
