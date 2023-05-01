# INFO314-UDPChat
Welcome! This is a group project assignment for my INFO314 course.

## Goals
In this project, you are going to use UDP to build a multiuser "chat" system that can broadcast messages to any number of participating clients. It will have (some of) the features of a modern chat system, but the principal goal here will be on the abilities (or lack thereof) of the UDP networking layer when compared to TCP.

In essence, you are going to build a server component, to which clients will connect. 

## Server
The server will provide "rooms" that clients can join, and messages sent from one client will go to all clients currently joined in that room. Messages may not go across rooms--what's said in a room is for the clients in that room only. Messages must always identify who they are from, and clients only see what messages are sent while they are in the room. (There is no sense of "persistent" message history.) 

## Client
Clients are unique, identified as a username/host-IP pair. (That is, a given user can only run one client on a given machine at a time.) When a client connects to a server, they should be presented with a list of the rooms on that server, and given the option to join.

## Stories/Rubric (20 pts)

* Server hosts 0 to n "rooms"
    * Rooms have a unique name (1 pt)
    * Rooms know what clients are in them (1 pt)
    * Rooms (names and clients) persist across server shutdown (2 pts)
* Client can always ask server what rooms are available (2 pts)
* Client can join (only one, max) room
    * If that room does not exist, it is created (1 pt)
    * If that room exists, client should now start receiving messages (1 pt)
* Client sending messages go to all clients in that room (3 pts)
* Do not lose any messages sent (2 pts)
* Clients not in a room do not get any messages from that room (3 pts)
* Messages always state which client they're from (2 pts)
* Client can quit a room
    * No more messages from that room are sent to that client (2 pts)
    * If no more clients are in a room, it remains (forever)

## Extra credit

* **Build unit tests for client and server: 1 pt** How would you test the client and/or server without needing to actually run the other side?
* **Build a "ghost" client: 2 pts** A "ghost" client is often used to log the messages sent within a given room without having to implement full message persistence for all clients. This kind of component is often used as an audit log of all messages sent, and in some cases can figure prominently in legal affairs.
* **Build an "admin" client: 2-4 pts** Admin clients are often "superuser" clients that have rights and abilities that the average client does not. In this system, an admin client can connect to any or all rooms simultaneously, though messages from the admin still only go to the room for which they are intended. (This means the UI for the admin client must be slightly different than the standard client, so the admin can indicate which room they wish to message.) An admin client that can see/message in all rooms simultaneously is worth 2 points. In addition, admin clients often have the ability to "kick" a client out of a room or off of a server entirely--if you implement this, it is worth 2 more points.
* **Secure transport: 5 pts** By default, traffic across UDP is sent "in the clear", and this could be problematic for a chat system. Use standard encryption libraries to encrypt traffic across UDP. You are free to impose whatever requirements you wish (each client having their own public/private keypair, for example), just be sure to document them.

