More standard functions
=======================

.. toctree::
   :maxdepth: 2


This page will go through some additionl functions, such as **sorted()**, **reversed()** and **map()**.

The sorted() function
---------------------

A very useful way to sort data. By default it works in a similar manner to the .sort() method used by lists.
::

    a_list = [1, 3, 5, 7, 9, 8, 6, 4, 2]
    
    print sorted(a_list)    #Note, this will return a new list
                            #i.e. does not change the value of a_list, like the list.sort() method

**output:**
::

    >>> run_demo_script.py
    
    [1, 2, 3, 4, 5, 6, 7, 8, 9]


+------------------------------+

+------------------------------+
   
-----

To make life easier, the **sorted()** function also has a **reverse** argument
::
    
    print sorted(a_list, reverse=True)

    # -> [9, 8, 7, 6, 5, 4, 3, 2, 1]
    

Sorted has other userful features
::

    num_list = range(100)
    num_list = map(str, num_list)  #using map to conver all values in num_list to str data type
                        #more on this later...
                        
    print sorted(num_list)

**output:**
::

    >>> run_demo_script.py
    
    ['0', '1', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '2', '20',..(etc).,'99']

You will notice the output here is a bit strange. Strings are sorted is alphanumerically, which means that all numbers beginning with '1' are sorted before those beginning with '2' etc.

+------------------------------+

+------------------------------+
   
-----

To fix this, we can set the criteria by which to sort by using the **key** argument.
::

    print sorted(num_list, key=int)
    
    # ->  ['0', '1', '2', '3', '4', '5', '6', '7', '8', ...(etc)... '97', '98', '99']   
    
Basically, here the 'int' function is applied to all elements in the list before sorting.
Note, that the list returned, still consists of string values.

+------------------------------+

+------------------------------+
   
-----

Likewise, we can sort based on length
::

    word_list = ['ant', 'cat', 'tower', 'dog', 'powder', 'frog', 'coward', 'log', 'jog', 'pizza']
    
    #First, without 'key' argument    
    print sorted(word_list) #without 'key' argument will produce an alphabetical sort
    
    #Now with 'key' argument
    print sorted(word_list, key = len) #Now it will sort, based onthe result of the len() function

**output:**
::

    >>> run_demo_script.py
    
    ['ant', 'cat', 'coward', 'dog', 'frog', 'jog', 'log', 'pizza', 'powder', 'tower']
    
    ['ant', 'cat', 'dog', 'log', 'jog', 'frog', 'tower', 'pizza', 'powder', 'coward']



Note, sorted() can also be applied to other data structures, such as strings
::

    print sorted('hello world')
    
    # -> [' ', 'd', 'e', 'h', 'l', 'l', 'l', 'o', 'o', 'r', 'w']

But note that it still returns a list of sorted characters. 



+------------------------------+

+------------------------------+
   
-----


The reversed() function
-----------------------

This function is something you would ONLY use when looping. It allows you to loop through a list, string etc in reverse order.
::

    my_list = [1, 3, 5, 7, 9, 11, 13, 15]
    for i in reversed(my_list):
        print i, 

**output:**
::

    >>> run_demo_script.py
    
    5 13 11 9 7 5 3 1


+------------------------------+

+------------------------------+
   
-----


Again, note, this is for looping ONLY. i.e. these cannot be used for comparisons etc.
::

    print reversed(my_list)
    
**output:**
::

    >>> run_demo_script.py
    
    <listreverseiterator object at 0x7f87bfa4fd50>




The map() function
------------------

The **map()** function allows you to execute a function on each element of a list. Below are a few examples using both functions and methods. 

First converting string values to integer values using the **int()** function
::
    
    my_str_list = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10']
    my_int_list = map(int, my_str_list)
    
    print my_int_list

**output:**
::

    >>> run_demo_script.py
    
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]   
    

+------------------------------+

+------------------------------+
   
-----


It is important to know what the output of a function is when using them. For example, **len()** returns an integer value
::

    word_list = ['ant', 'cat', 'coward', 'dog', 'frog', 'jog', 'log', 'pizza', 'powder', 'tower']
    len_list = map(len, word_list)
    
    print len_list

**output:**
::

    >>> run_demo_script.py
    
    [3, 3, 6, 3, 4, 3, 3, 5, 6, 5]


+------------------------------+

+------------------------------+
   
-----


Next, we will map methods. Since a method is a function that is specific to a class/object, we need to specify the class when mapping the method
::

    word_list = ['ant', 'cat', 'coward', 'dog', 'frog', 'jog', 'log', 'pizza', 'powder', 'tower']
    upp_list = map(str.upper, word_list)
    
    print upp_list

**output:**
::

    >>> run_demo_script.py
    
    ['ANT', 'CAT', 'COWARD', 'DOG', 'FROG', 'JOG', 'LOG', 'PIZZA', 'POWDER', 'TOWER']
    

+------------------------------+

+------------------------------+
   
-----


Again, it is important to keep track of the type of the data type returned by a function when using map. 
::


    word_list = ['ant', 'CAT', 'COWARD', 'DOG', 'frog', 'jog', 'log', 'PIZZA', 'powder', 'tower']
    is_up_list = map(str.isupper, word_list)
    
    print is_up_list

**output:**
::

    >>> run_demo_script.py
    
    [False, True, True, True, False, False, False, True, False, False]
