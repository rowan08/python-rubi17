File Generators
===============

.. toctree::
   :maxdepth: 2
   :caption: gen


This page shows how a generator function might be applied when reading information from files. Specifically, we will use the PDB file 1yuw.pdb in these examples. 


+------------------------------+

+------------------------------+
   
-----

Before we begin
---------------

Just a quick note: You can loop through a file without calling the **readlines()** method. A file is an iterable object in Python, meaning you can loop through it as you would loop through a list. You cannot, however, index it like a list or loop through it twice as you would a list, e.g. ::

    new_file = open('1yuw.pdb', 'r')

    for i in new_file:
        print i.strip()


**output:**
::

    >>> run_demo_script.py
    
    HEADER    CHAPERONE                               14-FEB-05   1YUW              
    TITLE     CRYSTAL STRUCTURE OF BOVINE HSC70(AA1-554)E213A/D214A MUTANT          
    COMPND    MOL_ID: 1;
        
    ... (etc) ...
    
    HETATM 4402  O   HOH A 673     -25.597  -7.669  -1.875  1.00 42.36           O  
    HETATM 4403  O   HOH A 674     -30.646  29.519  28.046  1.00 33.50           O 
    HETATM 4404  O   HOH A 675     -11.236  31.946  24.433  1.00 42.17           O  
    MASTER      292    0    0   19   29    0    0    6 4403    1    0   43          
    END

Now if we try run this same for-loop again
::    

    #second attempt
    print "\n\nSecond looping attempt"

    for i in new_file:
        print i.strip()

    #Note, nothing is printed because we have reached the end of the file...

    print "\nOne more looping attempt...\n"

    for i in new_file:
        print i.strip()

**output:**
::

    >>> run_demo_script.py
    
    Second looping attempt

    One more looping attempt...

    (*crickets*)


Just out of interest; the file object has a **seek()** method to allow you to move back to the beginning of the file. (or anywhere in the file really). 

**seek(0)** will go to the beginning, though...
::
        
    print 'resetting using seek()'    
    new_file.seek(0)

    print("\nLast try...\n")

    for i in new_file:
        print i.strip()

**output:**
::

    >>> run_demo_script.py
    
    resetting using seek()

    Last try...

    
    HEADER    CHAPERONE                               14-FEB-05   1YUW              
    TITLE     CRYSTAL STRUCTURE OF BOVINE HSC70(AA1-554)E213A/D214A MUTANT          
    COMPND    MOL_ID: 1;   
     
    ... (etc) ...
    
    HETATM 4402  O   HOH A 673     -25.597  -7.669  -1.875  1.00 42.36           O  
    HETATM 4403  O   HOH A 674     -30.646  29.519  28.046  1.00 33.50           O 
    HETATM 4404  O   HOH A 675     -11.236  31.946  24.433  1.00 42.17           O  
    MASTER      292    0    0   19   29    0    0    6 4403    1    0   43          
    END

+------------------------------+


+------------------------------+
   
-----

Writing generators for file reading
-----------------------------------

Using our generator logic, we can write a generator that yields values as it reads through a file. More importantly, it can do this when specific conditions are met, e.g.

SEQRES example
--------------
::

    def get_seqres(f):
        
        print '\nSeqres Extraction:\nOpening file %s' % f.name
        
        for line in f:
            if line.startswith('SEQRES'):
                yield line
            

    with open('1yuw.pdb', 'r') as new_file:

        for line in get_seqres(new_file):

            print line.strip()
                

**output:**
::

    >>> run_demo_script.py

    Seqres Extraction:
    Opening file 1yuw.pdb

    SEQRES   1 A  554  MET SER LYS GLY PRO ALA VAL GLY ILE ASP LEU GLY THR
    SEQRES   2 A  554  THR TYR SER CYS VAL GLY VAL PHE GLN HIS GLY LYS VAL
     
    ... (etc) ...
    
    SEQRES  42 A  554  ASP LYS VAL SER SER LYS ASN SER LEU GLU SER TYR ALA
    SEQRES  43 A  554  PHE ASN MET LYS ALA THR VAL GLU


+------------------------------+


+------------------------------+
   
-----

A more generalized example
--------------------------

This can be further generalized to loop through specific parts of a PDB file.  

::

    def get_lines(file_obj, identifier):
        
        print '\nGeneral Extraction:\nOpening file %s' % file_obj.name
        print 'Extracting %s information' % identifier
        
        for line in file_obj:
            if line.startswith(identifier):
                yield line
        
Obviously the two print-statements are not strictly necessary. They are only included to help show what the function is doing. Now let us test it out...

First let's see what happens if we set the identifier as 'ATOM'
::

    with open('1yuw.pdb', 'r') as new_file:

        for line in get_lines(new_file, 'ATOM'):

            print line.strip()
        
**output:**
::

    >>> run_demo_script.py
         
    General Extraction:
    Opening file 1yuw.pdb
    Extracting ATOM information

    ATOM      1  N   MET A   1      -0.688  28.039  -8.659  1.00108.11           N  
    ATOM      2  CA  MET A   1      -0.686  27.081  -7.519  1.00108.04           C  
    ATOM      3  C   MET A   1      -2.028  27.143  -6.792  1.00107.64           C  

    ... (etc) ...
    
    ATOM   4280  OE1 GLU A 554       6.939  -5.505  33.720  1.00137.66           O
    ATOM   4281  OE2 GLU A 554       7.065  -5.945  31.577  1.00137.69           O
    ATOM   4282  OXT GLU A 554       9.455  -3.863  36.636  1.00136.09           O


+------------------------------+


+------------------------------+

Now we set the identifier as 'HETATM':

::

    with open('1yuw.pdb', 'r') as new_file:

        for line in get_lines(new_file, 'HETATM'):

            print line.strip()

**output:**
::

    >>> run_demo_script.py
         
    General Extraction:
    Opening file 1yuw.pdb
    Extracting HETATM information   
    
    HETATM 4284  O   HOH A 555     -26.474   8.773  -1.079  1.00 10.89           O
    HETATM 4285  O   HOH A 556     -14.802  13.650  13.146  1.00  9.28           O
    HETATM 4286  O   HOH A 557      25.036  -0.072  31.041  1.00 16.67           O

    ... (etc) ...
        
    HETATM 4402  O   HOH A 673     -25.597  -7.669  -1.875  1.00 42.36           O
    HETATM 4403  O   HOH A 674     -30.646  29.519  28.046  1.00 33.50           O
    HETATM 4404  O   HOH A 675     -11.236  31.946  24.433  1.00 42.17           O
   
