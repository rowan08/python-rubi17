Generators
==========

.. toctree::
   :maxdepth: 2
   :caption: gen


This script provides an example of how a generator works. Running with this same example, the script also demonstrates \*args and \*\*kwargs as they appear in functions


+------------------------------+


+------------------------------+
   
-----

Before we begin
---------------

Just a quick demonstration of the value of using range() vs xrange()
If you were to uncomment and run the code below. The first sum, using xrange would maybe take 7 seconds to complete
The same sum() using range would most lkely crash your computer... So try it at your own peril...

::

    range_val = 1000000000
    print sum(xrange(range_val))
    print sum(range(range_val))

+------------------------------+


+------------------------------+
   
-----


Generator example
-----------------
::

    def xclone(start, stop, step):
                                        
        val = start   
        
        while val < stop:
            yield val
            val += step
            

(Note, this is not how xrange() works). 
Like range() and xrange(), we has set up our generator function to have a **start**, **stop** and **step**.
The generator will **yield** values with each iteration.

::

    print xclone(0, 11, 1)
    
    <generator object xclone at 0x7f6a75deb820>

You will notice that a generator object is returned. This is different to the output of the range() function, for example, which produces a list.

::

    print range(0, 11, 1)
    
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]


As with range() and xrange(), we can loop through the generator object returned by our xclone generator function.

::

    for i in xclone(0, 11, 1):
        print i,

    0 1 2 3 4 5 6 7 8 9 10

::

    for i in xclone(2, 10, 2):
        print i,

    2 4 6 8



+------------------------------+


+------------------------------+
   
-----


\*args and \*\*kwargs
=====================

\*args example
--------------

::

    def args_function(*args):
        
        print "The value of the tuple 'args' is:\n", args
        
        print "\nEach of the values in the tuple are as follows:"
        for i, v in enumerate(args):
            print "%s -> %s" % (i,v)
        print
            
    args_function(1, 2, 3, 'hello world', None, [1, 2, 3])

    
*args_function:*
Here **args**, will be a tuple containing all arguments given to the function.
This function will first print out the args list, then each element in the list.
The output of this code is as follows:

::

    >>> run_demo_script.py
    
    The value of the tuple 'args' is:
    (1, 2, 3, 'hello world', None, [1, 2, 3])

    Each of the values in the tuple are as follows:
    0 -> 1
    1 -> 2
    2 -> 3
    3 -> hello world
    4 -> None
    5 -> [1, 2, 3]

+------------------------------+


+------------------------------+
   
-----


xclone() with \*args and tuple unpacking:
-----------------------------------------

By using the \*args keyword we can design the function to cater for the following scenarios:

**1. Only 1 argument is given.** This is probably the most common use of range() or xrange()
In this instance, the input for the function should account for the **stop** argument.

-> e.g. **range(10)** produces the list 0-9. The **start** value 0 and the **step** value 1 are already implied 

Note, however, in the original version of our xclone() function; **stop** was set as the second input value. 
This makes it difficult to tell our function that the value of the argument is for **stop**.
To account for this, we design the function to act differently bases on the number of arguments it is given.

**2. Only 2 arguments are given**, corresponding to **start** and **stop**, respectively

-> e.g. **range(1, 11)** produces the list 1-10. The step value **1** is still assumed

**3. All 3 arguments are enterd**, corresponding to **start**, **stop** and **step**, respectively

::

    def xclone(*args):
                                        
        #args now will be a tuple of all arguments passed 
        # to the function
        
        if len(args) == 1:
            start, stop, step = 0, args[0], 1
        
        elif len(args) == 2: 
            start, stop, step = args[0], args[1], 1
        
        elif len(args) == 3:
            start, stop, step = args    #tuple unpacking example
            
        val = start   
            
        while val < stop:
            yield val
            val += step


::

    for i in xclone(1, 11): 
        print i,
    
    1 2 3 4 5 6 7 8 9 10

Because of \*args, it doesn't matter that we only give xclone() 2 arguments. Note, we still are assuming that the function takes 1, 2 or 3 arguments. Ideally the code should cater for these scenarios. 

+------------------------------+


+------------------------------+
   
-----


\*\*kwargs example
------------------

*kw_function:*
**kwargs** is a dictionary, where the key is the name of the argument used when calling the function.
And the value is the value we passed to the function. 

Its uses won't be as obvious at the moment, but it is useful to know what it does.
::

    def kw_function(**kwargs):
                                        
        print "kwargs dictionary:", kwargs

        print "\nIt has the following entries:"
        for key, value in kwargs.items():
            print ' -> Key:', key,
            print '\t value:', value


    #demonstration    
    kw_function(start=0, stop=1, x=5)

::

    >>> run_demo_script.py
    
    kwargs dictionary: {'start': 0, 'stop': 1, 'x': 5}

    It has the following entries:
     -> Key: start  value: 0
     -> Key: stop   value: 1
     -> Key: x      value: 5



+------------------------------+


+------------------------------+
   
-----


xclone function with \*\*kwargs
-------------------------------

This is a very poor/incomplete example of how \*\*kwargs can be used... don't do it!

::

    def xclone(**kwargs):
        
        if 'start' in kwargs:
            start = kwargs['start']
        else:
            start = 0
            
        if 'stop' in kwargs:
            stop = kwargs['stop']
        else: 
            raise TypeError('stop argument required')
            
        if 'step' in kwargs:
            step = kwargs['step']
        else:
            step = 1
            
        val = start   #Just adding this to make what's going on more clear
            
        while val < stop:
            yield val
            val += step


    for i in xclone(stop=11, start=1, step=1):
        print i,


::

    >>> run_demo_script.py
    
    1 2 3 4 5 6 7 8 9 10
