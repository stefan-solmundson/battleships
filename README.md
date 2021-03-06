# Battleships

This repository contains the code for playing a distributed game of Battleships using gRPC. It has a server component
as wel as a client component. 

## Setup
##### If you are using a virtual environment:  
Navigate to */venv/Scripts* & run ```activate.bat```.  
##### Regardless: 
Navigate to */server* & run ```pip install -r requirements.txt``` to install all of the required python dependencies.  

### Client 

The client contains a class which can be used to build a game client around. The `main.py` file contains a reference
implementation just to show how that could be done. 

### Server 

The server implementation is very loosely based on the Simon game, which can be found here: 
https://github.com/grpc-ecosystem/grpc-simon-says. However, that was written entirely in Go, while this is written in
Python. 

The game works like this:
1) A client first joins a game server, which then registers an open game;
2) A second client joins a game server, which joins an existing open game;
3) The game servers (one for each client) communicate using Redis (with the Game ID as the unique channel);
4) Clients play moves (i.e., attack a square) and report states (hit or miss), which are forwarded by the servers;
5) The game finishes when a client reports a 'defeat' (meaning Game Over).

Clients communicate with game servers using gRPC (a stream-stream connection). They send attacks and reports, and 
receive the result of their actions (hit/miss) and information about whose turn it is. 

## Running The Game - with Pycharm & Laragon
Laragon>Menu>Preferences..>Services & Ports>Tick: "Redis"  
<sub>Redis is effectively a temporary RAM JSON file used to store information & communicate between programs.</sub>  

Pycharm>Run>Edit Configurations...>  
Tick: Allow parallel  
// Name "main.py" files appropriately -so that they are easier to sort in the editor  

Now you can run a python file multiple times.
Use the stop button to keep track of what is running.
