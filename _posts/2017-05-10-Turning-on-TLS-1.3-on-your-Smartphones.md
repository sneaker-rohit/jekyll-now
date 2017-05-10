As we all know, Transport Layer Secuirty (TLS) is one of the most popular Internet security protocol.
Currently, TLS 1.2 is the most widely deployed TLS version on the internet. However, there are many
servers which continue to use older versions of SSL/TLS even today.

Recently, a new version - TLS 1.3 has been rolled out. TLS 1.3 improves the performance and security of
TLS. We know that TLS handshake takes 2 RTTs, post which the application data starts flowing. TLS 1.3
removes 1 RTT. This is a big improvement in terms of performance, especially for the mobile devices. From the
security point of view, TLS 1.3 removes all the vulnerable cipher suites completely. Therefore, you cannot turn
on any vulnerable stuff by any chance.

Below are the steps to turn on TLS 1.3 on your smartphones. Chrome Canary browser provides a mechanism to turn on
TLS 1.3.

I. Install Chrome Canary for your Android/IOS based Smartphone.

II. Open Chrome Canary and in the URL enter "chrome://flags"

![Chrome Canary](/images/flags.png){:class="img-responsive" height="500px" width="400px"}

III. Search for "Maximum TLS version enabled" and change if from "Default" to "TLS 1.3"

![Verify that TLS 1.3 is turned on](/images/cloudfare.png){:class="img-responsive" height="500px" width="400px"}

That's it. It's time to relaunch your browser :)

To verify, you can visit Cloudfare and click on the padlock icon on the left of the URL and click on "see details"
as shown in the figure below.

We can see that the connection is using TLS 1.3. In this example, we chose Cloudfare because they have already turned
on the support for TLS 1.3. TLS 1.3 deployment will eventually occur over the internet. Therefore, it's a long time
before we start seeing a plethora of servers using TLS 1.3.
