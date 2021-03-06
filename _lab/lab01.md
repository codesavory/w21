---
layout: lab
num: lab01	
ready: true
desc: "C++ class design to support CSV data"
assigned: 2021-01-13 
due: 2021-01-20 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives.  At the end of this lab, students should be able to:

-   read and understand  C++ code to read input from a CSV file
- 	read and understand  C++ code representing county demographic data
- 	extend an exisiting C++ class to support additional data and methods (including modifying related code to read in data)
-   be able to run provided test cases and understand the output to confirm code modifications work


Orientation
=====


Working with real world data allows us to use computing to ask questions and learn about our world.  It also allows us to practice design and implementation of object oriented projects.  This week's lab is the first step in our larger project related to using various data sources to learn about the United States.
This project and later additions will use the CORGIS datasets (The Collection of Really Great, Interesting, Situated Datasets): https://corgis-edu.github.io/corgis/

You will be provided with base code, written in C++ that reads in a CSV file representing county demographic data (demographic data relates to the structure of a population).  The data file we will use is included in the base code and is named  "county_demographics.csv."

Before you do anything else, goto the web page and take a quick look at all the data this csv file includes:
https://corgis-edu.github.io/corgis/csv/county_demographics/

Which aspects of this demographic data is most interesting to you?

We will only work with some of this data this quarter.  For today, we will only work with the data related to the age and education level of each county's
population.

Step by Step
============

Step 0: Getting Started
-----------------------

### Download base code and test the executables dataProj and testDemog1
Download the base code.  It can be found here:

https://github.com/ucsb-cs32-w21/lab01-STARTER

If you are set up to use git from the command line, you will be cloning: git@github.com:ucsb-cs32-w21/lab01-STARTER.git

As a reminder: If you are not familiar with git, I highly recommend learning this skill since this will be extremely valuable when collaborating on large software projects. More information on git can be found here: https://ucsb-cs32.github.io/topics/git/.

Once you have the files (and have created a git repo for this lab like last week), take a look at the files.

The starter code includes files related to our main data project and files related to testing our code.
When you try to compile the code using the provided Makefile, it should be able to make the executable for our main data project:
<b>dataProj</b> and testDemog1.

You should see some compilation errors related to building the testDemog2.  This is intentional (as you ultimately need to modify the class
definition - see later steps).

You should confirm that when you run
./dataProj

that it prints out county data (lots of county data - so expect you console to be filled with print outs).  You might see something like:

....

County Demographics Info: Uinta County, WY <br>
Population info: <br>
(% over 65): 11<br>
(% under 18): 29.8<br>
(% under 5): 7.6<br>
Education info: fix this for lab01<br>
<br>
County Demographics Info: Washakie County, WY<br>
Population info: <br>
(% over 65): 20.1<br>
(% under 18): 23.9<br>
(% under 5): 5.5<br>
Education info: fix this for lab01<br>
<br>
County Demographics Info: Weston County, WY<br>
Population info: <br>
(% over 65): 18.1<br>
(% under 18): 21.6<br>
(% under 5): 6.5<br>
Education info: fix this for lab01<br>
***<br>
Note that with so much data, it will likely be useful to redirect the output to a file.  If you run: Lab01Full zwood$ ./dataProj > outputFile
You can then open the text file "outputFile" to look at all the data using a text editor.
Or for example use "more outputFile" to examine the data one screen at a time.

You should also make sure that you can successfully run testDemog1 and see results like:<br>
[zjwood@csilvm-01 Lab01Base]$ ./testDemog1<br>
Testing class demogData...<br>
PASSED: c1.getName()<br>


Step 1: Read and Understand the code
-----------------------

### Lets take a look at the files (questions about these files is fair game for hw and quizzes this week)
Now, take a moment to look at the various files.
I suggest you start with main.cpp.
In your own words, how would you describe what main.cpp is doing?

Then take a look at our representation of county data:
demogData.h
demogData.cpp
You should note that at this time, we are only storing demographic information related to the age of the county population.
You will be editing and adding to this file, so make sure you understand it.

Next take at the helper functions used to read the data from our CSV file:
parse.h
parse.cpp
You will only have to make small modifications to these files, but should be able to understand the basics of how these
functions are working.

In general the above files will be a part of our project.  You will want to make friends with these files.  

The base code folder also includes some files for testing our code.
testDemog1.cpp
testDemog2.cpp
tddFuncs.h
tddFuncs.cpp

Take a quick look at the test files.  Test driven development helps us catch errors early in our code before we make assumptions and end up
in a dark corner (we still will have to debug but testing can help it be less painful).  
As mentioned above testDemog2 does not compile this is because you have some work to do.

Add comments to any of the files to help you remember what they do.  We will work with this code again this quarter so make sure to ask
questions now.


Step 2: Small modifications to the code (adding additional data to demogData)
-----------------------
### We will need to modify various files to add more demograpic data

Currently, the demogData class only stores data related to the age of the county's population.  
For this first week, lets add some additional information, specifically, the data related to education:
<b>Education.Bachelor's Degree or Higher <br>	
Education.High School or Higher</b>

There are a few closely related steps in this process:
1) add data to the class demogData to represent the percentage of the county population that have received an undergraduate degree and the percentage
that has graduated from high school
2) add the data fields to the class constructor (*add a new constructor for county data with all fields - leave the prior constructor and set default values for the education fields of -1).  You should have two constructors when you are done.*
3) add the necessary getter methods for this new data (hint: check out testDemog2 for getter names).
4) add code to parse.cpp to read in the two additional data fields (and use them when constructing a demogData object).
5) modify in demogData.cpp the function that overrides the << operator to also print the educational data.  See the below sample for formatting.

Finally, to start making the demogData class conform to good OO style, all the data is private, however, we want to give access to (read) the data, 
so add getters for all of the data currently associated with our demogData. (Note again see testDemg2 for getter names).

Step 3: Make sure your output matches and now all test cases pass
-----------------------
### Make and run
If you completed the steps above, you should now be able to compile all of the code and tests with <tt>make</tt>

So that when you run testDemog2 you see:

zwood$ ./testDemog2<br>	
Testing class county demographics...<br>	
PASSED: c1.getName()<br>	
PASSED: c1.getState()<br>	
PASSED: c1.getpopOver65()<br>	
PASSED: c1.getpopUnder18()<br>	
PASSED: c1.getpopUnder5()<br>	
PASSED: c1.getBAup()<br>	
PASSED: c1.getHSup()<br>	

Now, when you print all the county data it should look like:
...
County Demographics Info: Uinta County, WY<br>	
Population info: <br>	
(% over 65): 11<br>	
(% under 18): 29.8<br>	
(% under 5): 7.6<br>	
Education info: <br>	
(% Bachelor degree or more): 18.9<br>	
(% high school or more): 89.2<br>	
County Demographics Info: Washakie County, WY<br>	
Population info: <br>	
(% over 65): 20.1<br>	
(% under 18): 23.9<br>	
(% under 5): 5.5<br>	
Education info: <br>	
(% Bachelor degree or more): 23.6<br>	
(% high school or more): 90.5<br>	
County Demographics Info: Weston County, WY<br>	
Population info: <br>	
(% over 65): 18.1<br>	
(% under 18): 21.6<br>	
(% under 5): 6.5<br>	
Education info: <br>	
(% Bachelor degree or more): 17.2<br>	
(% high school or more): 90.2<br>	

Consider using <b>diff</b> on the file you produce and the provided comparison file.

Step 4: Submitting via Gradescope
-----------------------
### Submitting via Gradescope

The lab assignment "Lab01" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompSubmit your files with your github repo like last week.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

This lab is based entirely on the grade assigned by Gradescope. There may be labs this quarter where code style is assessed, but this is not one of those labs.

Gradescope automated

    (20 pts) each for all 5 of the Gradescope tests

Acknowledgements
================

Winter `21 vesion: Zoë Wood.  Thank you to the original CORGIS crew for their work sharing this data (https://corgis-edu.github.io/corgis/) and to Aaron Keen for curriuclum review. Editing, autograder and general support to thanks to: AMR, SDM, QH, AR, BL
