Server setup is based loosely on this guide: https://blogs.oracle.com/developers/post/how-to-set-up-and-run-a-really-powerful-free-minecraft-server-in-the-cloud

Shape used in instance:

<img width="597" alt="shape" src="https://github.com/Geckuss/OCI/assets/58637152/52b3e9cc-d27b-48cf-8aca-c90ddd54f633">

I am using Ubuntu server, as it is more widely used than Oracle Linux.

This processor uses ARM architechture, which provides better price/performance ratio, but causes multiple compatibility issues. Running one cloud instance on standard AMD or Intel processor would cost about 100$/month, while this shape is completely free! Another instance would cost only under 2$/month, but 4 cores and 24gb of ram is able to withstand multiple servers simultaneously. However, most game servers are made for x86, and need to be ported to ARM. Luckily, Java is very versatile and can be run on ARM out-of-the-box.

Boot volume used in instance (200gb is the limit for free tier):

<img width="714" alt="boot" src="https://github.com/Geckuss/OCI/assets/58637152/5c55bb31-cea9-4863-9693-fea744be093a">

Forwarded ports in virtual cloud network for needed network services:
-TCP and UDP for vanilla minecraft server
-TCP and UDP for console players connecting to vanilla minecraft server (Minecraft is not cross-platform, but with some server-side tweaks console players are able to connect to Java server)
-TCP port for Dynmap (3D-rendered online map)
-TCP and UDP for modded server

<img width="711" alt="pfw" src="https://github.com/Geckuss/OCI/assets/58637152/22b64450-b203-4c02-a664-c0defecc0d62">

Connection to server happens with PuTTY (or Bitvise or any other SSH client) + SSH:

<img width="218" alt="putty" src="https://github.com/Geckuss/OCI/assets/58637152/b4aacc59-1b5f-476c-86a6-131e4e8e9543">

Multiple servers running simultaneously in screens:

<img width="403" alt="screens" src="https://github.com/Geckuss/OCI/assets/58637152/1ba30ebc-7b62-49d5-82a0-4805acc9f5b3">

Connections to game servers happen via DNS (or public IP). Simultaneously running servers are separated with different ports:

<img width="366" alt="status" src="https://github.com/Geckuss/OCI/assets/58637152/80078d87-7b8f-4168-bfe5-ea858cf8473e">
<img width="453" alt="status2" src="https://github.com/Geckuss/OCI/assets/58637152/c81da033-06d1-42d7-8827-e2134538030d">

Interactive 3D render from game world is also running in the server:

<img width="960" alt="dynmap" src="https://github.com/Geckuss/OCI/assets/58637152/2e2615f6-8965-424a-a96e-4c7a5cf120d7">

Overview of contents in server folder:

<img width="646" alt="statech-files" src="https://github.com/Geckuss/OCI/assets/58637152/1b7a05b1-b1c8-4475-8d8f-21e115c8d9f1">

Server starts with this command automatically:

screen -dmS statech java -server -Xmx8G -jar fabric-server-mc.1.19.2-loader.0.14.22-launcher.0.11.2.jar nogui

Command starts screen instance named statech, allocates 8gb of ram, and runs server.jar file using Java without gui

