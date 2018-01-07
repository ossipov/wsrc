# WebSocket Remote Controller

Main idea behind this project is having secure remote access to data on remote  device without opening additional ports on that device. It can also be used to execute any command on that device.

## Why

I needed access to data on POS terminal and didn't want to allow incomming connections. So I thought of making a client app running on POS that connects to WebSocket Server and listens for commands from allowed sources. In short it's easy to think of it as a chat where one user send another user private message and gets needed response. 


## Components

* *Controlled Client (CC)* – all logic is written here and it can do literally anything you need. That script has to go on device you wish to controll. It has to be added to startup and should try to keep connection with WebSocket Server alive. (In my case it queries database and returns json response that is rendered on Requesting Client)
* *Requesting Client (RC)* — responsible of connecting to WebSocket Server, sending requests and render responses from Controlled Client.
* *WebSocket Server (WS)* — must be accessible by both clients. Plays the role of dispatcher between clients. It can be located on the Internet or home network.


## Requirements

* Nodejs / npm
* socket.io
* https
* fs
* pm2


## Installation

If you want to try things out and see how this work, you can install everything on your local device. 
```
git clone https://github.com/ossipov/wsrc
cd wsrc
npm install socket.io https fs 
pm2 start server.js controlled-client.js
pm2 log
```
WebSocket Server is started, Controlled Client is connected and we are looking on logs produced by both apps. Now start another console and run 
```
node request-client.js
```
Profit :)


## Projects that implement this idea

* *WSRC-Frontol* — Frontol is popular in Russia POS software. This project make data from POS available to authorized clients. 
