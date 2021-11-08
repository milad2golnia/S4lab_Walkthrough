Nowadays the use of proxies and VPNs is growing due to anonymity, bypassing censorship and etc. At the same time, the http proxies are dominating this area because of their simplicity to implement and use and also they’re faster than traditional VPNs.

Considering this situation there are so many public-free http proxies out there. One of the big question can be what the purpose of these public proxies is and **why someone should offer this free service**. In other hand we know when there is popularity to something and many people tend to use that one, you
can find so many attackers around it!

By using http proxies, people are trusting at a third party application to send all of their traffic through it and that’s where attackers are interested in. **An attacker can simply make a cloud-based virtual machine and build an Http proxy**, then he can register his proxy on public proxy list websites and alter
out/ingoing traffic.

At this articles, we are trying to find out how many proxies are honest and pass traffic without any modification. To achieve this goal, we monitored **15 public proxy list websites for two month** to get a list consist of **65871 proxies** (although not all of them were active).

At the next step, we deployed decoy websites (called *honeysites*) and tested each proxy against it. These
*honeysites* gives us advantages to avoid false positive result, because we have full control over them and
we can conduct experiment with different level of complexity but it can bring a risk to the experiment
too: What if some proxies are enough smart to identify *honeysites* and behave differently? To avoid this
risk, we use some real websites too such as www.bbc.com in this experiment.

The result of our research shows that **5.15%** of proxies are malicious. Furthermore we was able to
specify **what kind of malicious work each proxy does**, regarding this 5.15% of proxies we can group them
as below:
* 47% of malicious proxies do ad injection (replacing/adding ad or stealing revenue from original
ads).
* 39% of malicious proxies do some kind of fingerprinting.
* 12% of malicious proxies redirect users to malware page which can results in phishing attack.

Also we showed that some proxies can inject some codes which results in **full system compromising**.

But we didn’t stop at this point! We also **developed a service to recognize the safe and honest proxies by
scanning proxy list websites daily**. This service is available at https://proxyscan.ics.forth.gr.

**NOTE**: I didn’t see the service personally! It has security issue because it uses a certificate which is published for https://discs-svn.ics.forth.gr and not https://proxyscan.ics.forth.gr.