---
ID: 24
post_title: 'Sweet &#038; Swifty Animations'
author: rchatham
post_excerpt: ""
layout: post
permalink: >
  https://blog.reidchatham.com/2020/08/21/sweet-swifty-animations/
published: true
post_date: 2020-08-21 02:05:25
---
<div class="note-wrapper">

Escape the Pyramid of DOOM!

“In computer science, a data structure is a particular way of organizing data in a computer so that it can be used efficiently.” — Wikipedia

These data structures and design patterns let you escape the infamous anti-patterns with simple and generally useful solutions. Enter SwiftyAnimate (The Plug 🔌).
<h3 id="A better way to animate…">A better way to animate…</h3>
Have you ever tried to string together multiple animations? Yes, of course you have. You wrap each subsequent animation in the completion handler of the previous one and quickly end up writing additional functions just to break up the pyramid of doom (or wormhole of death?). No matter what you end up with it’s not really what you want. Maybe something like this…?
<pre><code class="code-multiline">UIView.animate(withDuration: time, animations: { [unowned self] in
    // animation
    self.animationFunction()
}) {  [unowned self] success in
    // non-animation function
    self.nonAnimationFunction()

    UIView.animate(withDuration: time, animations: {
        // animation
        self.animationFunction()
    }) { success in
        // function that takes time
        self.functionThatTakesTime {
            UIView.animate(withDuration: time, animations: {
                // animation
                self.animationFunction()
            }) { success in
                UIView.animate(withDuration: time, animations: {
                    // animation
                    self.animationFunction()
                })
            }
        }
    }
}</code></pre>
Pyramid of DOOM!

It’s even in the Apple Developer Documentation!!!

<a href="https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html">https://developer.apple.com/library/content/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html</a>

Enter Queues to the rescue! They give you O(1) time complexity for both enqueueing and dequeueing which you DO NOT get with the standard Array type in Swift (Arrays have O(1) average time complexity for append and popLast operations, where popFirst is an O(n) operation).
<pre><code class="code-multiline">internal class Node&lt;T&gt; {

    var data: T
    var next: Node&lt;T&gt;?

    init(data: T) {
        self.data = data
    }
}

internal struct Queue&lt;T&gt; {

    var first, last: Node&lt;T&gt;?

    mutating func dequeue() -&gt; T? {
        let pop = first?.data
        first = first?.next

        if first == nil {
            last = nil
        }
        return pop
    }

    mutating func enqueue(data: T) {
        if last == nil {
            first = Node(data: data)
            last = first
        } else {
            last?.next = Node(data: data)
            last = last?.next
        }
    }
}</code></pre>
Now we just add our animations to the queue…
<pre><code class="code-multiline">typealias Animation = (TimeInterval, ()-&gt;Void)

let animation: Animation = (5.0, {
    // Code to animate
})

let animations = Queue&lt;Animation&gt;()

animations.enqueue(animation)</code></pre>
…and recursively call the queue in each animation’s completion handler until it is empty.
<pre><code class="code-multiline">func perform() {
    guard let animation = animations.dequeue else { return }
    UIView.animate(withDuration: animation.0, animations: animation.1) { success in
        perform()
    }
}</code></pre>
Easy enough right?

If you want to take it further check this out. In SwiftyAnimate I wrapped our Queue struct in an Animate class. The Animate class enqueues animations, with the .then(duration: TimeInterval, animations: Animation) method, to a series of operations defined by the Operation enum (with animations being one of the cases). <b>the_code</b>
<pre><code class="code-multiline">// Escape the Pyramid of DOOM!

Animate(duration: time) { [unowned self] in
    // animation
    self.animationFunction()
}.do { [unowned self] in
    // non-animation function
    self.nonAnimationFunction()
}.then(duration: time) { [unowned self] in
    // animation
    self.animationFunction()
}.wait { [unowned self] resume in
    // function that takes time
    self.functionThatTakesTime {
        resume()
    }
}.then(duration: time) { [unowned self] in
    // animation
    self.animationFunction()
}.then(duration: time) { [unowned self] in
    // animation
    self.animationFunction()
}.perform()</code></pre>
Enjoy writing beautiful code! 🎉

</div>