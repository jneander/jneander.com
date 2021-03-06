---
title: == vs. eql vs. equals
description: Thoughts on the subtle differences between these three similar operators
redirect_from: 2012/07/21/==-vs-eql-vs-equals.html
---
It was suggested to me that it is common for Ruby developers to default to *==* when testing comparisons in their spec tests. This seemed odd to me, but it merited a little research in any case.

The operators act as follows
 - **==** returns true if two objects are equivalent, without regard for type or identity.
 - **.eql?** returns true if two objects have both equivalent value and type, regardless of identity
 - **.equals?** returns true if two objects are the same instance, having the same identity

{% highlight ruby%}
1.0 == 1
# => true

1.0.eql? 1
# => false

a = 1.0
b = 1.0
a.equals? a
# => true
a.equals? b
# => false
{% endhighlight %}

In testing, the operators differ only visually
 - **==** defers to the *==* method
 - **eql** uses the *.eql?* method
 - **equals** uses the *.equals?* method

As a rule of thumb: the longer the operator, the more restrictive the test it performs.

It may be true that programmers tend to use the *==* operator. For me, the information being compared - not personal style or preference - should be the deciding factor for the choice between one operator or another. After all, I want to be absolutely certain that my tests are passing for the right reasons.
