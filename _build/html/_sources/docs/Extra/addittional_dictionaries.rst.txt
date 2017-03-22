Additional dictionary
=====================

.. toctree::
   :maxdepth: 2
   :caption: gen

Small preamble
--------------

On the **'The enumerate() and zip() functions'** page, we went through using **izip()** to create a dictionary using two different lists.
::

    from itertools import izip
    
    nums = [1,2,3]
    words = ['one', 'two', 'three']
    
    my_dict = dict(izip(nums, words))
    
    print my_dict

**output:**
::

    >>> run_demo_script.py
    
    {1:'one', 2: 'two', 3:'three'}


The current page will not use this...
    
+------------------------------+

+------------------------------+
   
-----

Looping through dictionaries
----------------------------

Previously, we saw that looping througha dictionary involved looping through the keys in the dictionary. To access the values in this loop, we would access them using the keys, like so

::

    my_dict = {1:'one', 2: 'two', 3:'three'}
    
    for key in my_dict:
        value = my_dict[key]
        print key, value        


**output:**
::

    >>> run_demo_script.py
    
    1 one
    2 two
    3 three
    
    
+------------------------------+

+------------------------------+
   
-----
    
The items() method
------------------

Dictionaries come with a bulit-in method to make looping through both the keys and values easier.
::

    for key, value in my_dict.items():
        print key, value    

**output:**
::

    >>> run_demo_script.py
    
    1 one
    2 two
    3 three

    
+------------------------------+

+------------------------------+
   
-----

Similar to the **zip()** function, **items()** is highly inefficient; as it creates a new list containing tuples of each key-value pair in the dictionary. 
::

    print my_dict.items()
    
    [(1, 'one'), (2, 'two'), (3, 'three')]
    
    
+------------------------------+

+------------------------------+
   
-----

The iteritems() method
----------------------

For efficiency reasons, it is recommended to do this using **iteritems()**, which produces a generator. 
::

    for key, value in my_dict.iteritems():
        print key, value

**output:**
::

    >>> run_demo_script.py
    
    1 one
    2 two
    3 three
 
Again, this produces the same result, but the code is more efficienct and scales better.

+------------------------------+

+------------------------------+
   
-----

values() and itervalues()
-------------------------
::

    print my_dict.values()
    
    # -> ['one', 'two', 'three']
    
    #This is useful to see if a value is in your dictionary, 'e.g.'
    if 'three' in my_dict.values():
        print "I know my dictionary has the value three"

**output:**
::

    >>> run_demo_script.py
    
    I know my dictionary has the value three   

::

    if 'four' in my_dict.values():
        print "I know my dictionary has the value four"
    else:
        print "It would seem my dictionary does not contain the value four"


**output:**
::

    >>> run_demo_script.py

    It would seem my dictionary does not contain the value four
    
    
Again, though, if you wanted to loop through the values, it is recommended that you use **itervalues()** rather than values()
::

    for value in my_dict.itervalues():
        print value

**output:**
::

    >>> run_demo_script.py
    
    one
    two
    three


