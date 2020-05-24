+++
title = "TCP/IP"
date = "2020-05-24T21:59:04-04:00"
author = "Tom Konidas"
authorTwitter = "tomkonidas" #do not include @
cover = "img/tcp-ip.jpg"
tags = ["osi", "tcpip"]
keywords = ["networking", "tcpip", "protocols", "osi"]
description = "The fundamentals of networking always start with the TCP/IP and OSI models."
showFullContent = false
draft = true
+++

> The fundamentals of networking always start with the TCP/IP and OSI models.

Before we talk about these models, lets discuss what a network model even is:

> A network model is like a house blue print.

We used to have multiple models, vendor specific models, but since OSI (Open Systems Interconnection) was founded in the 1970s, 
we have grown accustomed to adopting an open standard all our networking gear could utilize to communicate with each other.

TCP/IP Comes from the DoD and was adopted in the 1990s which quickly replaced the OSI model.

### Why did TCP/IP replace the OSI?
OSI took too long to develope, TCP/IP had many volunteers so it took the lead in popularity and adoption.

The TCP/IP models creates a set of rules that allows us all to take a computer
(or mobile device) out of the box, plug in all the right cables, turn it on,
and connect to and use the network.

> Even though we do not use the OSI model in practice today, it is still very important to know amongst fellow engineers
> as it is very often refered to when chit-chating to other colleagues. 

Some fun sentences tht you can rememebr to help you with the layer's and their orders:
- People Don't Need Those Stupid Packets Anyway (My personal favorite)
- Please Do Not Take Sales People's Advice
- Please Do Not Throw Sausage Pizza Away
- Please Do Not Teach Students Pointless Acronyms

|Layer|OSI|TCP/IP|Layer|
|---|---|---|---|
|7|Application||
|6|Presentation||
|5|Session|Application|5|
|4|Transport|Transport|4|
|3|Network|Network|3|
|2|Data-Link|Data-Link|2|
|1|Physical|Physical|1|

> OSI's layers `5,6,7` is the same as TCP\IP's layer `5`

Every layer's job is to help the layer above.

## Application Layer

The application layer provides an interface between software runing on a computer and the network itself.

Examples:
- HTTP (Web Browsers)
- SMTP/POP3 (Email)

**HTTP** can be found in the browser's url. You use it all the time.
When you see status codes of `404` not found or `200` ok, these come from the application layer.

## Transport layer

Provides service to the application layer; the most popular protocols for this layer are TCP and UDP.

> Notice the `tcp` from **TCP**/IP comes from this layer as it is one of the most important layers along with the network layer which we will soon discuss.

An example service is the **TCP Error Recovery** service:
If  something happens and the browser does not get all the data, TCP is there to make sure it does. It uses acknowlegments to recover from error.

## Network Layer
Known for its IP (Internet Protocol); used for addressing and routing.

> This is where the TCP/**IP** gets it's `IP` from.

It is kind of like a postal service, it defines the details of where its coming from and where its going to.

Has a `source` and `destination` IP in the header.

## Data-Link & Physical

> Usualy bunched together since they work very closely.

Data-Link later consists of how its going to send. 
Such as:
- wifi
- Ethernet

The Physical Layer is the actual cabling and energy used to transmit the data.
Hardware examples include:
- Cables
- Hubs (Pretty old but still may find some in legacy networks)
- Repeaters

## Data Encapsulation

> Each layer adds its own header data.

|Layer|H/T (OSI)|A.K.A.|OSI|
|---|---|---|---|
|Transport (4)|Header (L4H)|Segment|L4PDU|
|Networking (3)|Header (L3H)|Packet|L3PDU|
|Data-Link (2)|Header,Trailer (L2H,L2T)|Frame|L2PDU|


> A little thing I use to remeber that a Frame has not only a header but a Trailer is to think of it being sandwitched between two things. Looking at it through a frame where it is closed on both sides.