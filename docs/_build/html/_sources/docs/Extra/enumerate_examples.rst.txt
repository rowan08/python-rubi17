The enumerate() and zip() functions
===================================

.. toctree::
   :maxdepth: 2
   :caption: gen


This page gives some basic examples of how the **enumerate()** and **zip()** functions work. It will also show the related function, **izip()**, provided by the **itertools** module.


+------------------------------+

+------------------------------+
   
-----

Looping through a string
------------------------

Much like looping through the elements in a list, we can loop through the characters in a string using a fairly straight-forward for-loop

::

    my_string = "Hello world"
    
    for i in my_string:
        print i,        


**output:**
::

    >>> run_demo_script.py
    
    H e l l o   w o r l d
    
+------------------------------+

+------------------------------+
   
----- 
  
We can also loop through the index positions of each character in the string as follows
::

    for i in range(len(my_string)):
        print i,
    
**output:**
::

    >>> run_demo_script.py
    
    0 1 2 3 4 5 6 7 8 9 10
    
    
+------------------------------+

+------------------------------+
   
----- 
    
What if we need to know the position and value of each character while we loop through the string? 
::

    for i in range(len(my_string)):
        char = my_string[i]
        print i, char
    
**output:**
::

    >>> run_demo_script.py
    
    0 H
    1 e
    2 l
    3 l
    4 o
    5  
    6 w
    7 o
    8 r
    9 l
    10 d

    
+------------------------------+

+------------------------------+
   
----- 

The enumerate() function
------------------------

A better way to do this is just to use the **enumerate()** function.    
::

    for i, char in enumerate(my_string):
        print i, char
        
**output:**
::

    >>> run_demo_script.py
    
    0 H
    1 e
    2 l
    3 l
    4 o
    5  
    6 w
    7 o
    8 r
    9 l
    10 d
    
+------------------------------+

+------------------------------+
   
-----
    
So if we wanted to know the postion of all 'l' characters in the string we could do the following
Note, I am using the shorthand **i**, **v** instead of **index**, **value**. Either is find (you can call these variables what you like...)
::

    lpost_list = []
    
    for i, v in enumerate(my_string):
        if v == 'l':
            lpost_list.append(i)
    
    print lpost_list

**output:**
::

    >>> run_demo_script.py
    
    [2, 3, 9]

To confirm that this works...
::

    for i in lpost_list:
        print my_string[i],    

**output:**
::

    >>> run_demo_script.py

    l l l
        
+------------------------------+

+------------------------------+
   
-----
     
Note, we can also make use of this with list comprehension
::

    lpost_list_2 = [i for i,v in enumerate(my_string) if v == 'l']    
    
    print lpost_list
    print lpost_list_2

**output:**    
::

    >>> run_demo_script.py
    
    [2, 3, 9]
    [2, 3, 9]
    
    
+------------------------------+

+------------------------------+
   
-----

Looping through multiple lists in tandem
----------------------------------------

What about looping through two list at the same time? Let us say we want to link the values **[1, 2, 3]** to the words **['one', 'two', 'three']**. Since both lists are the same length, we could just do the following
::

    num_list = [1, 2, 3]
    word_list = ['one', 'two', 'three']

    for i,v in enumerate(num_list):      

        num_val = num_list[i]
        word_val = word_list[i]
        
        print num_val, word_val  
        

**output:**    
::

    >>> run_demo_script.py
    
    1 one
    2 two
    3 three        
       
    
+------------------------------+

+------------------------------+
   
-----

       
The zip() function
------------------

A useful altenative, however, is to use the **zip()** function
::

    for num_val, word_val in zip(num_list, word_list):
        print num_val, word_val    
        
**output:**    
::

    >>> run_demo_script.py
    
    1 one
    2 two
    3 three        
       
    
+------------------------------+

+------------------------------+
   
-----        

Assembling a dictionary using zip()
-----------------------------------

Of course, this type of relationship is more useful as a dictionary. Note, the following
::

    num_dict = dict(zip(num_list, word_list))   #sets each element in num_list as a key
                                                # and corresponding value in word_list as a value          
                                                
    print num_dict

**output:**    
::

    >>> run_demo_script.py
    
    {1: 'one', 2: 'two', 3: 'three'}



Inefficiency of zip()
---------------------

The **zip()** function creates a new list of tuples corresponding to the positions of each element in each list given to the function. If two or more large lists are given to the function, it can use an unnecessarily large quantity of memory for this, e.g.
::

    print zip(range(10000), range(10000,0,-1))  #not a great example of zip()

    [(0, 10000), (1, 9999), (2, 9998),... (etc)..., (9997, 3), (9998, 2), (9999, 1)]



The izip() function
-------------------

Based on the ineficient nature of the **zip()** function, it is recommended that **izip()** be used instead, e.g.
::
    
    from itertools import izip
    
    for i, k in izip(range(10000), range(10000,0,-1)):
        print i, k

    0 10000
    1 9999
    2 9998

    ... (etc)...
    
    9997 3
    9998 2
    9999 1


                             
