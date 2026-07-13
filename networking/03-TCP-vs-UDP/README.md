# 🚀 TCP vs UDP

> **TCP (Transmission Control Protocol)** and **UDP (User Datagram Protocol)** are the two primary transport layer protocols of the TCP/IP Model.
>
> They define **how data is transmitted between applications over a network**.
>
> Choosing the right protocol directly impacts **reliability, speed, latency, and application performance**.

---

# 📖 Table of Contents

- What are TCP and UDP?
- Why Do We Need Them?
- Problem They Solve
- TCP vs UDP Comparison
- How TCP Works
- How UDP Works
- TCP Three-Way Handshake
- Sequence Numbers & ACKs
- Real-World Analogy
- Production Examples
- DevOps Perspective
- Common Interview Questions
- Common Mistakes
- Summary

---

# What are TCP and UDP?

Both TCP and UDP operate at the **Transport Layer (Layer 4)** of the TCP/IP Model.

Their responsibility is to deliver data from one application to another.

Examples:

```
Browser
      │
HTTP
      │
TCP
      │
IP
      │
Internet
```

or

```
DNS Client
      │
UDP
      │
IP
      │
Internet
```

The main difference is:

- **TCP prioritizes reliability**
- **UDP prioritizes speed**

---

# Why Do We Need Them?

Different applications have different requirements.

Imagine you're making a video call.

Would you rather:

- Wait for every lost packet to be retransmitted?
- Or continue the call smoothly even if one frame is lost?

Now imagine online banking.

Would you accept losing a transaction packet?

Of course not.

Some applications require **perfect reliability**.

Others require **minimum delay**.

That's why both protocols exist.

---

# Problem They Solve

Without transport layer protocols:

- Applications wouldn't know whether data arrived.
- Lost packets couldn't be retransmitted.
- Multiple applications couldn't communicate simultaneously.
- There would be no concept of ports.

TCP and UDP solve these problems differently.

---

# TCP vs UDP

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection | Connection-Oriented | Connectionless |
| Reliability | Guaranteed | Not Guaranteed |
| Packet Order | Preserved | Not Guaranteed |
| Error Recovery | Yes | No |
| Acknowledgements | Yes | No |
| Retransmission | Yes | No |
| Speed | Slower | Faster |
| Overhead | Higher | Lower |
| Streaming | Poor | Excellent |
| Video Calls | Not Preferred | Preferred |
| Banking | Preferred | Not Preferred |

---

# How TCP Works

TCP establishes a connection before sending any data.

It guarantees reliable communication using:

- Sequence Numbers
- Acknowledgements (ACK)
- Retransmission
- Flow Control
- Congestion Control

If a packet is lost,

TCP automatically resends it.

This makes TCP reliable.

---

# Sequence Numbers & ACKs

One of the biggest interview questions is:

> **How does TCP actually guarantee delivery?**

Every byte sent by TCP receives a **Sequence Number**.

Example

```
Packet 1
Sequence = 1000

Packet 2
Sequence = 2000

Packet 3
Sequence = 3000
```

The receiver replies with an ACK.

```
ACK = 3000
```

Meaning:

> "I successfully received everything up to byte 3000."

If the sender doesn't receive an ACK before the timeout,

it retransmits the missing packet.

This mechanism is what makes TCP reliable.

---

# TCP Three-Way Handshake

Before sending application data,

TCP first establishes a connection.

```
Client                      Server

SYN  ---------------------->

      <-------------------  SYN + ACK

ACK  ---------------------->

Connection Established
```

### Step 1

Client sends **SYN**

"I want to start communication."

---

### Step 2

Server replies

**SYN + ACK**

"I received your request and I'm ready."

---

### Step 3

Client sends

**ACK**

"I received your acknowledgement."

Now both sides know communication works in both directions.

Data transmission begins.

---

# Why Three Messages?

Think of making a phone call.

Person A:

"Can you hear me?"

↓

Person B:

"Yes, I can hear you. Can you hear me?"

↓

Person A:

"Yes."

Conversation begins.

The handshake verifies that **both devices can send and receive data** before actual communication starts.

---

# How UDP Works

UDP is much simpler.

There is:

- No Handshake
- No ACK
- No Retransmission
- No Packet Ordering

The sender simply transmits packets.

```
Client

Packet

Packet

Packet

Packet

↓

Network
```

If one packet is lost,

UDP never asks for it again.

This makes UDP extremely fast.

---

# Real-World Analogy

## TCP

Sending a registered courier.

You receive:

- Tracking Number
- Delivery Confirmation
- Signature

If delivery fails,

the courier sends it again.

Reliable but slower.

---

## UDP

Throwing paper airplanes.

Some arrive.

Some don't.

Nobody checks.

Nobody resends.

Extremely fast.

---

# Production Examples

## TCP

- HTTPS
- SSH
- FTP
- Git Clone
- Database Connections
- Email

Whenever data accuracy matters,

TCP is preferred.

---

## UDP

- DNS Queries
- Video Streaming
- Live Sports
- Voice Calls
- Online Gaming
- IoT Devices

Whenever latency matters,

UDP is preferred.

---

# Why Does DNS Use UDP?

A DNS lookup usually consists of:

Client

↓

Question

↓

Server

↓

Answer

One small request.

One small response.

If one packet is lost,

asking again is cheaper than creating a TCP connection.

Therefore,

DNS generally uses UDP.

---

# Why Don't Video Calls Use TCP?

Suppose one video packet gets lost.

TCP stops the stream,

waits,

retransmits,

then continues.

The result:

Frozen video.

Poor user experience.

UDP simply skips the missing packet.

The next video frame arrives immediately.

A slightly blurry frame is much better than freezing the entire call.

---

# DevOps Perspective

Understanding TCP vs UDP is essential for:

- Kubernetes Services
- Docker Networking
- AWS Security Groups
- Load Balancers
- Firewalls
- NGINX
- API Communication
- Troubleshooting

Examples:

| Service | Protocol |
|----------|----------|
| SSH | TCP |
| HTTPS | TCP |
| Kubernetes API | TCP |
| DNS | UDP |
| Syslog | UDP |
| Streaming | UDP |

---

# Common Interview Questions

### Q1. Why is TCP reliable?

Because it uses:

- Sequence Numbers
- ACKs
- Retransmission
- Flow Control

---

### Q2. Why is UDP faster?

Because it doesn't establish a connection,

doesn't wait for acknowledgements,

and never retransmits lost packets.

---

### Q3. Why does DNS use UDP?

DNS requests are very small.

Using UDP avoids the overhead of establishing a TCP connection.

---

### Q4. Why don't video calls use TCP?

Retransmitting lost packets introduces delay.

For real-time communication,

low latency is more important than perfect reliability.

---

### Q5. Does UDP have ports?

Yes.

Both TCP and UDP use **Port Numbers**.

---

### Q6. Which protocol does HTTPS use?

HTTPS runs over **TCP**.

---

# Common Mistakes

❌ TCP is encrypted.

✅ TCP is **not encrypted**.

Encryption is provided by **TLS**, not TCP.

---

❌ UDP has no ports.

✅ UDP uses ports just like TCP.

---

❌ TCP guarantees zero packet loss.

✅ TCP cannot prevent packet loss.

It detects packet loss and retransmits missing packets.

---

❌ DNS always uses UDP.

✅ DNS primarily uses UDP but can switch to TCP for large responses, DNS zone transfers, or when UDP responses are truncated.

---

# Summary

TCP and UDP are the two transport layer protocols responsible for application-to-application communication.

TCP focuses on **reliability**, ensuring every packet reaches its destination through acknowledgements, sequence numbers, and retransmissions.

UDP focuses on **speed**, sending packets without waiting for confirmations, making it ideal for real-time communication.

Choosing between TCP and UDP depends on the application's requirements.

If reliability is critical, use TCP.

If low latency is critical, use UDP.

---

## 🔗 Related Topics

⬅️ Previous: **TCP/IP Model** → `../02-TCP-IP-Model/README.md`

➡️ Next: **Browser to Server Flow** → `../04-Browser-to-Server/README.md`

📖 Recommended Reading:

- OSI Model
- TCP/IP Model
- HTTP vs HTTPS
- DNS
