+++
title = "TCP/IP Fundamentals"
date = "2020-05-24T16:48:52-04:00"
author = "Tom Konidas"
authorTwitter = "tomkonidas"
cover = "img/tcp-ip.jpg"
tags = ["osi", "tcpip"]
keywords = ["networking", "tcpip", "protocols", "osi"]
description = "The fundamentals of networking always start with the TCP/IP and OSI models."
showFullContent = false
draft = false
+++

> The fundamentals of networking always start with the TCP/IP and OSI models.

Before we talk about these models, lets discuss what a network model even is:

Put simply, a network model is like a house blue print.
Another way to think of it is like a nice big cake. Where each layer adds its own flavor to the mix.

We used to have multiple models, vendor specific models, but since the [OSI (Open Systems Interconnection)](https://en.wikipedia.org/wiki/OSI_model) was founded in the 1970s by the International Organization for Standardization (ISO),
we have grown accustomed to adopting an open standard all our networking gear could utilize to communicate with each other.

[TCP/IP](https://en.wikipedia.org/wiki/Internet_protocol_suite) comes from the DoD and was adopted in the 1990s which quickly replaced the OSI model.
By the 2000s, it dominated all networks and became the primary model. It is what's used to this very day.

### Why did TCP/IP replace the OSI?

The OSI took too long to develop and the TCP/IP had many volunteers, so naturally it took the lead in popularity and adoption.

The TCP/IP models creates a set of rules that allows us all to take a computer
(or mobile device) out of the box, plug in all the right cables, turn it on,
and connect to and use the network.

> Even though we do not use the OSI model in practice today, it is still very important to know amongst fellow network engineers
> as it is very often referred to when chit-chatting to other colleagues.

Some fun sentences that you can use to help remember the layer's order:

- People Don't Need Those Stupid Packets Anyway (My personal favorite)
- Please Do Not Take Sales People's Advice
- Please Do Not Throw Sausage Pizza Away
- Please Do Not Teach Students Pointless Acronyms

| Layer |     OSI      |   TCP/IP    | Layer |
| :---: | :----------: | :---------: | :---: |
|   7   | Application  |             |       |
|   6   | Presentation |             |       |
|   5   |   Session    | Application |   5   |
|   4   |  Transport   |  Transport  |   4   |
|   3   |   Network    |   Network   |   3   |
|   2   |  Data-Link   |  Data-Link  |   2   |
|   1   |   Physical   |  Physical   |   1   |

> OSI's layers `5,6,7` is the same as TCP\IP's layer `5`

Every layer's job is to help the layer above.

## Application Layer

The application layer provides an interface between software running on a computer and the network itself.

Examples:

- HTTP (Hypertext Transfer Protocol)
- SMTP/POP3 (Email)

**HTTP** can be found in the browser's url. You use it all the time.
When you see status codes of `404` not found and `200` ok, these come from the application layer.

This is the layer I have interacted with as a software developer; Making calls to REST Apis and such.

Open your browsers dev tools (`F12`), go to the network tab and refresh the page.
Here you can see all the network calls and their status.

![Firefox Dev Tools HHTP Status](/img/network-http-status-devtools.PNG)

[Here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) is a list of the standard HTTP responses codes if you are more curious on this subject.

## Transport layer

The Transport layer provides service to the application layer; the most popular protocols for this layer are TCP and UDP.

> Notice the `tcp` from **TCP**/IP comes from this layer as it is one of the most important layers along with the network layer which we will soon discuss.

An example service is the **TCP Error Recovery** service:
If something happens and the browser does not get all the data, TCP is there to make sure it does. It uses acknowledgments to recover from error.

This layer is like a bridge with a traffic controller, it gathers all the messages from the application and transmits them into the network.

## Network Layer

Known for its IP (Internet Protocol); used for addressing and routing.

> This is where the TCP/**IP** gets it's `IP` from.

Think of this layer as a postal service, it defines the details of where its coming from and where its going to.

It adds a header to the segment with a `source` and `destination` IP.
This is called a **Packet**.

## Data-Link & Physical

> Usually bunched together since they work very closely.

The Data-Link layer consists of how its going to send.
Defining technologies such as:

- wifi
- Ethernet

This layer adds both a Header and Trailer to the packet, which then becomes a **Frame**.

Some important information held in the Frame header are MAC addresses. That is the unique address give to a device.
They look something like `00:AB:43:12:CC:21`. The first 3 bytes are provided by the IEEE to a vendor (called the OUI -> Organizationally unique identifier), this is because every MAC must be unique so
vendors request a number and the IEEE provide them. Any vendor that wants to sell hardware must go through the process of registering and obtaining a OUI from the IEEE.
The manufacturer then adds another 3 bytes to the end ny their own choosing for products.
This is very interesting because you can know the vendor of a device by looking up the first 3 bytes of a MAC address.

The Trailer in the Frame is used for Error Detection (**Note this is not error recovery, ONLY detection**)

The Physical Layer consists of the actual cabling and energy used to transmit the data.
Hardware examples include:

- Cables
- Hubs (Pretty old but still may find some in legacy networks)
- Repeaters

## Data Encapsulation

Each layer adds its own header data from the previous layer.
Then the layer after reads it and generates its own header (or Trailer if L2PDU) and adds upon that.
The data inside does not matter at the points, it does not care whats inside only the headers/trailer that surround it.

This concept is a familiar one from programming.

|     Layer      |        H/T (OSI)         | A.K.A.  |  OSI  |
| :------------: | :----------------------: | :-----: | :---: |
| Transport (4)  |       Header (L4H)       | Segment | L4PDU |
| Networking (3) |       Header (L3H)       | Packet  | L3PDU |
| Data-Link (2)  | Header,Trailer (L2H,L2T) |  Frame  | L2PDU |

Once it goes from application to physical, then across the network.
It works in reverse order on the other side and performs data decapsulation in the reverse order starting from layer 1 to 5.

> A little trick I use to remember that a Frame has not only a header but a Trailer is to think of it being sandwiched between two things. Looking at it through a frame where it is closed on both sides.
