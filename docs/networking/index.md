# Networking

服务器和客户端之间的通信是一个成功 Mod 必不可少的一部分.

网络通信中有以下两个主要目标:

1. 确保客户端视角与服务端视角 "同步"
    - 位于 (X, Y, Z) 的花正在生长
1. Giving the client a way to tell the server that something has changed about the player
    - 玩家按下了一个键

The most common way to accomplish these goals is to pass messages between the client and the server. These messages will usually be structured, containing data in a particular arrangement, for easy sending and receiving.

There is a technique provided by NeoForge to facilitate communication mostly built on top of [netty]. This technique can be used by listening for the `RegisterPayloadHandlersEvent` event, and then registering a specific type of [payloads], its reader, and its handler function to the registrar.

[netty]: https://netty.io "Netty Website"
[payloads]: payload.md "Registering custom Payloads"
