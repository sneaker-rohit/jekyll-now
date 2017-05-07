The motivation of this post is to brief about using utilities such as rkhunter and chkrootkit to hunt down rootkits.

With the ever-increasing number of attacks on systems, it is indispensable for system administrators to keep an eye on the malicious softwares being installed on their system. Rootkit Hunter and Chkrootkit are two popular utilities that can help to hunt down rootkits.

Rootkits are the softwares that make the operating system believe that the system files are as expected and there is no malicious activity going on. Rootkits serve as a layer of shield for the virus and the malware so that they can remain undetected by the antivirus softwares. 

The packages for debian systems can be installed with the package name as rkhunter and chkrootkit.

sudo apt-get install rkhunter 

This installs rootkit hunter. In order to run rkhunter, you can type 

rkhunter --check 

This will begin the process of scanning your system. Keep pressing enter to allow rkhunter to perform multiple level of checks. There's a lot more you can do with rkhunter. Just enter rkhunter --help and explore :)

To install and run chkrootkit, just enter 

sudo apt-get install chkrootkit 

chkrootkit 

chkrootkit is a shell script that checks system binaries for rootkit modifications.