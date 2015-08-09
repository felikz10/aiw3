# aIW3 #

A powerful and scalable networking library based on the Quake 3 Protocol for enthusiasts.

**Requires:** Python 2.5 or greater

This module was used in the development of the **AlterIWNET** _Call of duty: Modern Warfare 2_ client / server communication.


---


### Minimal implementation example utilizing AlterIWNet servers ###

```
from aIW3 import *

#Create a aIW() object, but don't connect anywhere yet.
handle = aiw()

#Grab all the aIW servers in our proximity.
#You have the option of using handle.grab_server_list_local()
#Or using aiw.grab_server_list().
#The difference is that the class method grab_server_list_local()
#Fetches the server list directly from servers.alteriw.net by default.
#While grab_server_list() fetches the server list directly from
#http://alteriw.net/hlsw.php by default. grab_server_list_local() is faster
#But grab_server_list() will retrieve the complete server list.
serverList = handle.grab_server_list_local()

#Connect to every server in our list and parse the response.
for server in serverList:
    try:
        handle.Connect(server) #server = "ip:port"
        responseA = handle.command("getstatus")
        responseB = handle.command("getinfo")
        parsedA = aiw.prepare_for_lobby(responseA)
        parsedB = aiw.get_players_online(responseB)
        joined = aiw.join_responses(parsedA, parsedB)
        print joined
        #print "fetched %s out of %s" % (serverList.index(server), len(serverList))
    except:
        print "server timed out."

#Close our socket when we are done working.
handle.close()

```