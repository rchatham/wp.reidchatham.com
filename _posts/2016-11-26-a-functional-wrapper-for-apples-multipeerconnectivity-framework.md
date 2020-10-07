---
ID: 38
post_title: >
  A functional wrapper for Apple’s
  MultipeerConnectivity framework.
author: rchatham
post_excerpt: ""
layout: post
permalink: >
  https://blog.reidchatham.com/2016/11/26/a-functional-wrapper-for-apples-multipeerconnectivity-framework/
published: true
post_date: 2016-11-26 17:02:00
---
<p><a href="https://cocoapods.org/pods/PeerConnectivity">PeerConnectivity</a> is a framework that I wrote for simplifying the code needed to write Bluetooth/Wifi networking across iOS devices. It it currently published on Cocopods and is also available for download via Carthage.</p>
<p>If you have ever used Apple’s MultipeerConnectivity framework you know you are in for a world of hurt. There are so many moving parts that it quickly becomes difficult to manage large networking operations between devices. As I was using it in a larger application I began writing wrappers to encapsulate the functionality of the framework and to keep it contained while remaining accessible. Thus… PeerConnectivity was born.</p>
<h4>Setup Connection Manager</h4>
<p>Setting up a connection manager to automatically find and connect with nearby devices is as easy as passing in the specified service type (similar to channel).</p>
<pre><code>let pcm = PeerConnectionManager(serviceType: &quot;local&quot;)</code></pre>
<h4>Starting/Stopping</h4>
<p>Start and stop with a single command.</p>
<pre><code>pcm.start()
// Session active
pcm.stop()
// Session inactive</code></pre>
<h4>Sending Events to Peers</h4>
<p>Sending events is as simple as creating JSON packets and passing them to the network or specified peer.</p>
<pre><code>let event: [String: Any] = [
    &quot;EventKey&quot; : Date()
]
// Sends to all connected peers
pcm.sendEvent(event)
// Access the connected peers to send to specific peer devices
if let somePeerThatIAmConnectedTo = pcm.connectedPeers.first {
   pcm.sendEvent(event, toPeers: [somePeerThatIAmConnectedTo])
}</code></pre>
<h4>Listening for Events</h4>
<p>Register event listeners to respond to incoming peer events.</p>
<pre><code>// Listen to an event
pcm.observeEventListenerFor(&quot;someEvent&quot;) { (eventInfo, peer) in
    print(&quot;Received event \(eventInfo) from \(peer.displayName)&quot;)
    guard let date = eventInfo[&quot;eventKey&quot;] as? Date else { return }
    print(date)
}
// Stop listening to an event
pcm.removeListenerForKey(&quot;SomeEvent&quot;)</code></pre>
<p>This makes for an extremely lightweight networking syntax that makes implementing mesh-networking in your app simple. Enjoy 😸. </p>