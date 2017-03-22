Unpacking tuples
================

.. toctree::
   :maxdepth: 2


tuples have an interesting property in Python. Their values can be 'unpacked' to declare several variables at a time. This is actually what happens when we looping using enumerate() and my_dict.items(). 

Tuple unpacking
---------------

Effectively, what it is doing is the following
::

    my_tuple_list = [(1, 'a'), (2, 'b'), (3, 'c')]
    for num, letter in my_tuple_list:
        print num, letter
   


**output:**
::

    >>> run_demo_script.py
    
    1 a
    2 b
    3 c


+------------------------------+

+------------------------------+
   
-----

This can generalize to quite large numbers. Just to demonstrate, assume each tuple had 5 elements
::

    my_tuple_list = [(1, 'a', 'puppy', 2.3, None), (2, 'b', 'kitty', '9.9', True), (3, 'c', 'Fishy', 3.142, False)]
    
    for val_1, val_2, val_3, val_4, val_5 in my_tuple_list:
    
        print "%s \t %s \t %s \t %s \t %s" % (val_1, val_2, val_3, val_4, val_5)
    
**output:**
::

    >>> run_demo_script.py
    
    1 	 a 	 puppy 	 2.3 	 None
    2 	 b 	 kitty 	 9.9 	 True
    3 	 c 	 Fishy 	 3.142 	 False


+------------------------------+

+------------------------------+
   
-----

The alternative to this code would be the following
::

    for next_tuple in my_tuple_list:
        
        val_1, val_2, val_3, val_4, val_5 = next_tuple
    
        print "%s \t %s \t %s \t %s \t %s" % (val_1, val_2, val_3, val_4, val_5)

Which, again, produces the same output
**output:**
::

    >>> run_demo_script.py
    
    1 	 a 	 puppy 	 2.3 	 None
    2 	 b 	 kitty 	 9.9 	 True
    3 	 c 	 Fishy 	 3.142 	 False


This is why sometimes you wil see someone do the following
::
    
    a, b = 1, 2

    print a
    # -> 1

    print b
    # -> 2

Python achieves this with tuple unpacking

It is an important concept to understand with using functions that return tuples or lists of tuples, such as enumerate() etc...

This can also be used to do a safe simultanious update, e.g. with the fibonnaci sequence question
::

    x = 0
    y = 1
    print x
    print y
    for i in range(18):
        x, y = y, x+y
        print y

**output:**
::

    >>> run_demo_script.py

    0
    1
    1
    2
    3
    5
    8
    13
    21
    34
    55
    89
    144
    233
    377
    610
    987
    1597
    2584
    4181

The above code will produce numbers in the fibonnaci sequence.

The following will not...
::

    x = 0
    y = 1
    print x
    print y
    for i in range(18):
        x = y
        y = x+y
        print y

**output:**
::

    >>> run_demo_script.py

    0
    1
    2
    4
    8
    16
    32
    64
    128
    256
    512
    1024
    2048
    4096
    8192
    16384
    32768
    65536
    131072
    262144    
    
    
This is because Python evaluates the right-hand side of the expressing before assigning values to the variable, which is a handy feature of tuples.
