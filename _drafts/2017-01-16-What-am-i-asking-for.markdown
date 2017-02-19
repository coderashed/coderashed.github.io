---
layout: post
title:  "What am I asking for?"
date:   2017-01-16 08:05:46 -0800
categories: jekyll update
---

<p>
I am often trying to find ways of no longer having to programmatically decypher what is wrong when something does not work in an application. How am I suppose to be able to account for all of the things that could go wrong?
It is foolish to try. This is however, usually where the conversation stops. But why is it foolish to try? The reason is simply because <strong>often times the system that we are trying 
to understand, is not our system to understand in the first place!</strong> Here is where the concept of <strong>object state</strong> comes in to play.
</p>

> Objects simply represent the <strong>state</strong> of something. <strong>State</strong> is simply the status of something at an instant in time. If each object manages its own state, no one fights with each other.

<p>
For the purpose of illustrating my point, I will represent objects as people. When repeatedly using words like me and my, I am trying to personify the objects in your mind. 
Objects each have their own job. Objects should be stingy! <strong>State</strong> is not to be shared!
</p>
<p>
If the <strong>state</strong> is not owned by me, then it is not my state to try to understand. With everyone following this rule, there is very little 
<strong>state</strong> to be managed by any single individual. Code complexity becomes inherently simple 11and reusable object patterns are easy to implement because one object cannot break the <strong>state</strong> of another.
</p>
<p>
Since <strong>state</strong> is such an abstract concept, I will show some common examples of it being mismanaged:
</p>
<br />
<h2>File Handling</h2>
<p>Are you checking to see if a file exists? Why do you need to check? What do you intend on doing with the file?</p> 
<p>Consider the following...</p>
<ul>
 <li>Are you including code into a script and trying to avoid an error or warning if it does not exist?</li>
 <li>Are you going to write to the file?</li>
 <li>Are you going to read the file?</li>
 <li><strong>Do we really need to query the system yourself to see if the file exists before doing any of these?</strong></li>
</ul>
<p>
One does not always consider the fact that generally speaking, and especially today, the filesystem has drifted out of the direct control of the language that we are interfacing with (in this case, PHP.)
</p>
<p>
<strong>Now consider the following...</strong>
</p>
<ul>
 <li>What can we tell our interfaces to tell us?</li>
 <li>PHP has all of these notices and warnings that we are often told are <em>safe to ignore</em></li>
 <li><strong>Maybe the system is actually trying to <em>tell</em> us something!</strong></li>
</ul>
<br />
<h2>Memory Access</h2>
<p>
Are you checking to see if an array index exists before accessing it? This may <em>sound</em> strange to ask but why would someone access an index before accessing the same index?
That is what we are asking the system to do! And we <em>usually</em> don't even feel bad about it! 
</p>
<p>
This may sound repetitive, <em>maybe</em> it is suppose to.
</p>
<p>
<strong>Now consider the following...</strong>
</p>
<ul>
 <li>What can we tell our interfaces to tell us?</li>
 <li>PHP has all of these notices and warnings that we are often told are <em>safe to ignore</em></li>
 <li><strong>Maybe the system is actually trying to <em>tell</em> us something!</strong></li>
</ul>
<br />
<h2>State Caching</h2>
<p>
Where this act may not be inherently bad, it is almost always unnecessary where done, as well as implemented in a way that causes more problems than it solves.
Let us use a common database mistake as an example of where this can go wrong in a simple and well intended way.
Have you seen data pulled from a single database into memory, in order to use code to see if it is unique before inserting a new record? 
Now consider what will happen when a duplicate record is inserted by someone else, in between the time you have pulled the data, and the time you run your insert?
</p>

<p>
<strong>Now consider the following...</strong>
</p>
<ul>
 <li>What modes of error handling can you tell the state owner to use to <strong>tell</strong> you when a problem occurs?</li>
 <li>What types of errors will the various database table constraints raise and what do they <strong>tell</strong> you?</li>
 <li>How can you catch and handle these errors <strong>after</strong> they occur?</li>
</ul>

<p>
Usually the first two examples are fairly harmless. They result in excess code complexity and a double dip into filesystems and memory structures. 
</p>
<p>
<strong>The last example however,</strong> will result in application breaking bugs that can be extremely difficult to find and solve. Especially 
so when they (as they often do) result from core architectural issues with their software. 
</p>
<p>
Life is easier when we don't manage the things that aren't ours to manage. Let us instead work towards pushing as much <strong>state</strong> as 
possible out of the hands of our application logic. That way, we leave the business logic for the business!
</p>

<p>
In my next post, we explore some ways to do just that and push <strong>state</strong> to the appropriate system mechanisms. This allows us to code like lazy slobs 
and our code is actually better/faster and more bug free for it!
</p>

<p>Up next, <strong>What can you tell us?</strong></p>