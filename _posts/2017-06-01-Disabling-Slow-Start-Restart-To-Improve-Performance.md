In this post, I will walk through what slow start in TCP is and why we should disable slow start restart on our servers.

What is Slow Start?

Let's make this simple. Imagine you had to send 100 packets from system A to system B and you want this task to be done as quickly as possible. Let's have a look on what goes on under the hood when an application sends this data (which is 100 packets in total) to another machine. So, TCP as we all know is the transport protocol that applications rely on for sending the data in a reliable way. Let's have a look at how TCP performs this data transfer.

The sending host knows about what the receiver can handle. This is because the receiver had advertised this window when it started communicating with the sending host. However, what is unknown is the number of packets that the network can handle. The network is dynamic and the sender must try to probe the network to understand on how many packets can it handle.

So, the source begins by sending 1 packet and waits for an acknowledgement. On receiving the ack, it increments the window size by 1. So, now the window size is 2 packets and the source sends 2 packets and waits for its ack. On receiving the ack for 2 packets, it now increments the window to 4. This process goes on in a similar fashion. So the window would go on from 1,2,4,8,16,32,64 and so on until there is a packet drop. This method of probing the network to know how much it can handle is known as slow start. A packet drop indicates that the network cannot handle more than this amount and the source must not double its window any further. Then, TCP jumps to Additive Increase Multiplicative Decrease (AIMD) phase. For the sake of simplicity, we will avoid the discussion of AIMD and Fast retransmit. For now, all you should understand is that these are another 2 phases that a TCP enters into during its operation.

So, let's come back to slow start. The point to see here is that why is it that we start with 1 and then go on to double. Why can't we start directly with 100? That would help us send the packets faster right? In fact, in our scenario here we would accomplish transmission in just one transfer. Unfortunately, this is considered too aggressive and would result in packet loss. However, researchers at Google have announced that the initial congestion window must be set to 10 and not 1.

According to Ilya Grigorik, a web performance engineer at Google, "Increasing the initial cwnd size on the server to the new RFC 6928 value of 10 segments (IW10) is one of the simplest ways to improve performance for all users and all applications running over TCP. And the good news is that many operating systems have already updated their latest kernels to use the increased value — check the appropriate documentation and release notes.For Linux, IW10 is the new default for all kernels above 2.6.39."

Therefore, by now I believe I have communicated the idea of slow start and why you should have the initial congestion window set to a minimum of 10.

Let's explore now what slow start restart is ;)

Slow start restart (SSR) is a mechanism that will reset the congestion window to default when the connection has been idle for a long time. Imagine, you were not exchanging any data and were idle most of the time, in this situation SSR is going to set the congestion window to default and the reasoning behind this is pretty simple that the network conditions must have changed by now. However, disabling SSR has proven to be useful for many cases and you should consider to disable it to gain some performance benefits.

To view the current settings you can type,

`sysctl net.ipv4.tcp_slow_start_after_idle`

The value must be set to 0. If it's not set, you can do it by

`sysctl -w net.ipv4.tcp_slow_start_after_idle=0`

That's all for this post. Do keep an eye on my posts for some more performance hacks :)