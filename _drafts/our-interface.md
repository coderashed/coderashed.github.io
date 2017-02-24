<h1>What are we working with?</h1>

<p>
This step is almost always skipped, but by building an understanding of our interface (PHP) before we get started we are learning the following 
very important things:
</p>
* Which methods our interface has of informing us of problems.
* What responsibilities we can push off of ourselves and on to the system internals. (This can drastically increase code readability and performance)
* Where if at all will our interface fight our personal coding style?
* Can the interface be configured in ways that better fit our goals? 
* <b>Is the interface appropriate for our goals at hand?</b>

<p>
Notice that if the above is considered without bias or other ill fated emotions then this logic can be applied to <b>any</b> language.
Be practical in your decision of which language to use when writing your application. Consider the talent you have on hand for instance.
It doesnt make much sense to pick a language if no one has experience with it. Since there is no one here to argue with me, I have picked PHP. 
We do however have some issues to address first.
</p>

<h2>What are you trying to tell me?</h2>

<p>
I can't tell you how many times I have read something along the lines of, "That is just a notice. You can ignore it."
I won't name names here, but lets take a step back and examine a couple of these notices or warnings...
</p>

<code>
<?php
$foobar = array('foo' => 'foo');
echo $foobar['bar'];
</code>
This causes:
PHP Notice:  Undefined index: bar in /home/coderashed/foo.php on line 3

<code>
<?php
include_once('some-nonexistant-file');
</code>
This causes:
PHP Warning:  include_once(some-nonexistant-file): failed to open stream: No such file or directory in /home/coderashed/bar.php on line 2
PHP Warning:  include_once(): Failed opening 'some-nonexistant-file' for inclusion (include_path='.:/usr/share/php') in /home/coderashed/bar.php on line 2


<p>
Is this not useful knowledge? Why would we want to ignore all of this? Why would we want execution to continue without intervention?
I would rather trap these messages and leverage this in my design to mean that my user did something wrong, and act upon it. Now 
how do we do this...?
</p>

<h2>Our First problem</h2>

<p>
We may not know <b>how</b> we are going to solve our problem yet, but we have identified <b>what</b> the solution to the problem is. Let's lay it out:
</p>
* We want to be able to catch PHP notices and warnings in the form of an <a href="http://php.net/manual/en/class.exception.php">Exception</a> object.
* To be able to tell them apart, we will call them PHPError objects and they will extend Exception.
* We will do the same to be able to tell our most common errors apart as well (PHPNotice,PHPWarning)

Now that we know what we want to accomplish, we begin our discovery process for <b>how</b> we want to accomplish it. 
