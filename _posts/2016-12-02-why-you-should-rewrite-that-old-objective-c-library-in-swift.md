---
ID: 43
post_title: >
  Why you should rewrite that old
  Objective-C Library in Swift
author: rchatham
post_excerpt: ""
layout: post
permalink: >
  http://blog.reidchatham.com/2016/12/02/why-you-should-rewrite-that-old-objective-c-library-in-swift/
published: true
post_date: 2016-12-02 17:13:59
---
<p>I recently came across an issue in the interoperability of two Objective-C API’s that I was using from a Swift app. One was known to be rewritten in Swift soon but was very trusted and widely used (JSQMessagesViewController) while the other a much smaller but also well tested framework that had not been updated in a long time (VENTokenField). I wanted to use these two frameworks together to create a new message interface much like the one in the standard messages app but due to a few features they could not be directly used together in the situation in part because of a bug that was going to take a massive amount of fiddling to work around.
I took a good long look at the situation at hand. JSQMessagesViewController’s keyboard observer looks for a UITextView as opposed to VENTokenPicker using a UITextField and so to have the toolbar follow the keyboard properly I was either going to have to work a UITextView into the inner workings of the VENTokenPicker or I was going to have to do the reverse with the keyboard observer.
Needless to say, I wanted to do it in Swift because my app was in Swift. I looked at the total code and figured the VENTokenPicker could be rewritten in a total of 3 files in Swift. The whole initial go took 1 day of my time to get it working and another day to smooth out most of the bugs and get the final touches right. I thought not bad. In that time I fixed the bug, rewrote a good but old Objective-C library that wasn’t getting much love into a new Swift one, converted the UITextField into a UITextView (arguably the more correct option), did not have to fiddle significantly with JSQMessagesViewController as the alternative option would’ve forced me to do, and get to feel good about myself as a member of the open source community (<strong>pat myself on the back</strong>).
Now, there are a lot of hiccups when converting code from Objective-C to Swift but at the very least this exercise will give you a better understanding of the differences between the languages and at best make you look like a Swift hero 🤗! I expect if you translated something directly as closely as you could translate it from Objective-C to Swift it would crash immediately…. but keep going, you got this!!!
Check out TokenField in Swift on <a href="https://github.com/rchatham/TokenField">Github</a> or <a href="https://cocoapods.org/pods/TokenField">Cocoapods</a>. </p>