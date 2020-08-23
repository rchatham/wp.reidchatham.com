---
ID: 41
post_title: >
  Mesh Networking for a Better User
  Experience
author: rchatham
post_excerpt: ""
layout: post
permalink: >
  http://blog.reidchatham.com/2016/12/01/mesh-networking-for-a-better-user-experience/
published: true
post_date: 2016-12-01 17:09:04
---
<p>You see mesh-networking implemented in many of the top apps these days, for example Snapchat uses mesh-networking to help you to find and add people nearby. But why is this not a standard practice? And why not for more types of data? To me it seems like it will be soon, but for now it requires developer time to implement and debug, so is it worth it?</p>
<p>You’ll see in Snapchat that both users must have navigated to the screen dedicated for finding people nearby in order for it work. On the other hand, Airdrop is the standard for sharing images or files between devices and you only need to have yourself set to discoverable and have your bluetooth on. You even see apps at the extreme, with the entire functionality of the app based on it’s use, such as Firechat for offline messaging and games like Spaceteam.</p>
<p>This isn’t by accident. Mesh-networking provides a significantly better experience for sending data than email or text messages and can deliver information directly between devices securely. It saves your feed from clutter and stores the new data where you want to access it.</p>
<p>On the other hand automatic implementations of mesh-networking can be problematic because it makes a user’s presence available to anyone in the area and can introduce security concerns if too much data is made available for free.
Using mesh-networking to be able to add contacts, find local users, facilitate offline inter-device communication, and lightening the networking load on a device are all great examples of ways that you can improve your user experience and simplify the function of your app.</p>
<p>If you’re not already convinced that mesh-networking is the future, at least to consider trying it out in one of your own apps. I built an open source library designed to make implementing mesh-networks simple and painless. If you are looking for a library to get you started and let you leverage some of the advantages of adding mesh-networking to your app you can check out my open source library called <a href="https://medium.com/@rchatham/peerconnectivity-71ef96477abe">PeerConnectivity</a> on <a href="https://github.com/rchatham/PeerConnectivity">Github</a> and <a href="https://cocoapods.org/pods/PeerConnectivity">Cocoapods</a> (The Plug. 🔌). Any suggestions or thoughts are greatly appreciated! </p>