---
title:  Speed Up Network Connection--Based on a Cloud Computer Located in Tokyo
tags: 折腾Z-Turn
---

## Background and Some Basic Information

This guide is designed to help some readers improve their Internet connection speed. For some reasons, this guide is written in English. 

The default readers of this article should meet the following description:

 - Willing to increase the connection speed of some websites (including Google Scholar, Wikipedia, etc.)
 - Live in East Asia
 - Can afford a certain amount of expenses
 - Understand some basic computer operations

Normally, after completing the instructions provided in this tutorial (It takes no more than one hour), you will be able to connect to some websites at a faster rate. 

If you find it's hard for yourself to finish all these steps or you find that you need other help, just feel free to contact me by mail or WeChat.

We believe that a free Internet can help us understand the world better.

## First Step: Deploy a Server

Considering the convenience and cost, we recommend purchasing a cloud server on Vultr, BandwagonHost or DigitalOcean. For convenience, let's take Vultr as an example to briefly describe the process of purchasing a cloud server.

This step takes no more than 10 minutes.

 - Visit [Vultr](https://www.vultr.com/?ref=8621342) (Referral Link), Click sign up in the upper right corner to register an account.
 - After logging in, enter the main page and click the blue plus button to add a VPS server.
 - Choose your server as Cloud Computer:
   - server location: Tokyo or New York
   - server type: Debian 10 x64
   - server size (Tokyo): $5/month
   - server size (New York): \$3.5/month or \$5/month
 - Choose Deploy Now, you can find Alipay and WechatPay in Billing. 

After returning to the products option, you can find a new cloud instance. You need to wait for its Status to change from Installing to Running before you can use it. Click directly on Cloud Instance to enter to view server information. We can see important options such as Ip Address, Username and password. The next step is to build a proxy server.

## Second Step: Build a Proxy Server

Because we can destroy the server (and deploy a new one) or reinstall the server at any time we like in vultr, it's no need to worry about making mistakes in the next few steps.

This step takes no more than 10 minutes.

 - Let's assume that you are using a windows system, download [Putty](https://the.earth.li/~sgtatham/putty/0.72/w64/putty.exe). And you can ask me for help if you are not using a windows system and we know each other in real life.
 - After opening, directly enter the IP address provided in the server information in the host name column, and click open to start the connection. When the first connection warning window appears, directly select Yes. 
 - Login as the username provided by server information, which is root, then directly enter the password and log in.(It is important to note that in putty, a copy is made by right-clicking the mouse button, and you cannot observe the copy result when you copy the password.)
 - After successfully entering the server, we begin the installation of the shadowsocks service.

## Third Step: Installation of Shadowsocks Service

Although the configuration of shadowsocks is a bit complicated for beginners, in most application scenarios, we only need to install the script to complete the setup process.

This step takse no more than 15 minutes.

Firstly, you need to input following instruction in the putty and press enter to install the script. 

>wget https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh 

Secondly, we need to change its permissions to make it run, enter following instruction to add executable permissions to the script.

>chmod +x shadowsocks-all.sh

After that, we can enter following instruction to enter the automatic installation process.

>./shadowsocks-all.sh

At this stage, we need to set some basic rules for shadowsocks, and we list these basic rules as follow:

 - Version: shadowsocks-libev (Recommend), enter 4 to choose this version.
 - Password: Default or any password you like. (Remember it)
 - Port: Default (Recommend) (Remember it)
 - Encryption: Default (aes-256-gcm) (Recommend)
 - Obfs: N (Not necessary for us to use obfs, so we choose NO)

Finally, we need to press Enter to confirm the automatic installation and configuration. And if all these installation are finished, we can just enter the final step.

## Final Step: Installation of Shadowsocks Client

After the third step, we need to run the shadowsocks client on the computer or mobile phone to connect to the server. We can download it by:

 - [Shadowsocks for Windows System](https://github.com/shadowsocks/shadowsocks-windows/releases/download/4.1.7.1/Shadowsocks-4.1.7.1.zip), visit this [website](https://github.com/shadowsocks/shadowsocks-windows/releases) if you meet any problem.
 - [Shadowsocks for Android](https://github.com/shadowsocks/shadowsocks-android/releases/download/v4.8.3/shadowsocks--universal-4.8.3.apk), visit this [website](https://github.com/shadowsocks/shadowsocks-android/releases) if you meet any problem.
 - We recommend you use Potatso Lite or Shadowrocket if you use iPhone, however, to install these two applications, you may need to have an apple account in the United States.

After running the windows client, a small airplane icon will appear in the task bar at the lower right corner. Right-click to enter the server option and select edit server. Fill in the ip address of your cloud computer and the port, password and encryption method (aes-256-gcm), click OK to connect.

The settings of the mobile client are basically the same. Click the plus button in the upper right corner and select manual settings to enter various information.

So far we have completed the setting of the server and client. Although it looks very long, Almost all operations are just copy and paste, we only need to do a few things.

Then, what you need to do is visit [Google](https://google.com), normally, you will be able to connect this website at a faster rate.

Finally, I would like to end this article with an irrelevant sentence.

>But there will be no gloom for her who was in anguish. &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ISAIAH 9:1
