*Portland Code School*
#Ruby Code Challenge 4


## Overview


You are given a file of tab-separated names and phone numbers, named "raw_customers.txt". The file is several thousand lines long. The names and numbers seem to be in a variety of formats.

You need to "clean up" this data, breaking down the names into their component parts and making all the phone numbers into the same format. You will need to write a simple analysis script to determine some information about the data, then you have to write a script that cleans the data.

You will be paired as in earlier code challenges. 

You and your pair must deliver the tests, code, the prefix words file, and the cleaned output file in a github repo named code_challenge_04 by the deadline the class sets for itself after reviewing this specification. That's right, you and you classmates need to set your own deadline and meet it.

## Required concepts

### Regular Expressions 

This code challenge is solved with one or more **regular expressions**. As you loop through the file, you use a regular expression to recognize the component parts of the data and remember them for output. For example, if the names all looked like this:

    first last

a regular expression that would identify the two components starting at the beginning of the line and store them in match groups so they can be output later would look like this:

    ^(\S+) (\S+)

Your regular expression will have to deal with more complex situations, described below. You may be able to write several regular expressions that look for different patterns. That's up to you. 

### Resources

See [Blue Box Tutorial](https://www.bluebox.net/insight/blog-article/using-regular-expressions-in-ruby-part-1-of-3) and/or the [NetTuts+ tutorial](http://net.tutsplus.com/tutorials/ruby/ruby-for-newbies-regular-expressions/).

Use [Rubular](http://www.rubular.com) to develop your regular expressions. 

The [Pickaxe Book](http://ruby-doc.com/docs/ProgrammingRuby/html/intro.html#S5) has good material about regular expression [here](http://ruby-doc.com/docs/ProgrammingRuby/html/language.html#UJ) and [here](http://ruby-doc.com/docs/ProgrammingRuby/html/tut_stdtypes.html#S4).

### Command line options

use OptionParser

See Chapter 2 of the exerpt: [Build Awesome Command Line Applications In Ruby](ref/build-awesome-command-line-applications-in-ruby.p1_0-exerpt.pdf)

### Object-oriented design

A *file* has one or more *lines*. Each line has a *name* and a *number*. A name should be able to initialize itself from a string, ignore irrelevant parts of the string, and report its components. It should report *nil* if the name doesn't have that particular component. A number should be able to initialize itself from a string and to report itself in th preferred format. Name and number objects should *not* be able to output themselves to STDOUT or a file. Use separate logic for I/O.

Example

    # you can split the line at the tab into two halves

    name = Name.new (first_half_of_the_raw_line_from_file)
    puts name.first_name
    phone_number = PhoneNumber.new (second_half_of_the_raw_line_from_file)
    puts phone_number.number, phone_number.extension

##Processing

### First step: analysis. 

Typically, you write routines to characterize the data. You need to answer the question, "What are the prefixes?" 

Write some code that uses a regular expression and a loop to collect all the first words of the lines and create a histogram. A histogram is a list of words with their frequency - how often they appear. Sort it from the most common word to least common word. 

Your script will be invoked like this:

    ruby analyze.rb <raw_customers.txt >histogram.txt

Notice how the script reads from STDIN and prints to STDOUT. This is the simplest form of command line input and output. 

Pipe the histogram to a file. The file might look like this:

    Ms. 422
    Mr. 321
    Miss 224
    George 120
    Jane 90
    Biggles 1

Examine the file for the likely candidates for prefixes and remove the others. Save the file as "prefix_words.txt" because you will use the file of prefixes later. It might look like this:

    Ms.
    Mr.
    Miss

(Testing to see if the first word in the line is a prefix makes it easier to deal with a wide variety of first names.)

The rest of the analysis has been performed by somebody else. Here are the results:

The format of the names looks to be something like:

    [prefix] [first_name] [middle_name | middle_initial] last_name [suffix]

where: 

* Everything in [square brackets] is optional. 
* There may be a middle name or a middle initial, but not both. 
* If there is a middle name or a last name, there will be a first name. (For "M. Jackson", "M." is the first name.)
* There is always a last name (For "Miss Jane," "Jane" is a last name)
* Sometimes the last name is hyphenated (as in "Dr. Huntington-Smythe"). Do not split hyphenated last names.

The phone numbers come in a variety of formats: some with hyphens, some with a prefix, some with parentheses. They all appear to be USA numbers, tho.

### Second step: cleaning. 

You will need to write a script that will be invoked like this:

    ruby clean.rb --prefixes prefix_words.txt --input raw_customers.txt --output customers.csv

or

    ruby clean.rb -p prefix_words.txt -i raw_customers.txt -o customers.csv

Your script must output usage and help information and exit if it is given bad arguments or is invoked like this:

    ruby clean.rb --help

or this:

    ruby clean.rb -h


## Testing

For this code challenge, you will write Rspec tests ('specs') and you *must* follow test-driven development practices. 

There are several types of that you need to write:

0. Write specs that verify your name initialize method and regular expression can recognize various name formats that match the analysis above. 
0. Write more specs that verify that you can output the different parts of names correctly. 
0. Write more specs that verify that you can recognize all the different formats of phone numbers.
0. Write even *more* specs that verify that you can output phone numbers.
0. Write specs that prove your command line arguments do what they are supposed to do, including detecting bad arguments
0. Write specs that prove you can input a small file of sample data and output a file of clean data.

Follow test-driven-development methodology and *prove that you have done so* by committing each test prior to creating the code that makes it pass. 

    # write a spec
    git commit
    # make it pass by writing code
    git commit

    # rinse, repeat.

Your repository *must* tell the tale of test-driven development. One test at a time, and the code to make that test pass next. If you don't do this, you will feel like a schmuck if you have any sense of professionalism at all. If you *are* able to do this, you will feel like the gods and goddesses of Olympus, returned in triumph to the adulations of your minions and the appreciation of your future employers.


## Style guide

All of your committed files should pass rubocop with no offenses. Do this early and often (see the above testing requirement). Don't commit code that doesn't pass rubocop.


## Required output

Your script must output a comma-separated file, each line in the following format (<angle brackets> indicate the value of a variable):

    <prefix>, <first_name>, <middle_name_or_initial>, <last_name>, <suffix>, <phone_number>, <extension>

The first line must contain column headings in snake case, suitable for use in another script. For example:

    prefix, first_name, middle, last_name, suffix, phone_number, phone_extension

No matter what format the raw phone number is in, it must only be output to the file in the following format:

    +1.nnn.nnn.nnnn 

with the extension in a separate column

###Example

Input lines

    Mr. Jenkins                     155.258.9944
    Mrs. Dameon C. Thiel            223-109-2182 x381
    Miss Clifton Cummerata-Smith    816.364.7371
    Caitlyn R. Corwin DVM           (652)817-0236 x47143


Output lines (notice how some columns are blank)

    prefix, first_name, middle, last_name, suffix, phone_number, phone_extension
    Mr.,,,Jenkins,,1.155.258.9944,
    Mrs.,Dameon,C.,Thiel,,1.223.109.2182,381
    Miss,Clifton,,Cummerata-Smith,,1.816.364.7371,7371
    ,Caitlyn,R.,,Corwin,DVM,1.652.817.0236,47143

<hr />
Copyright © 2013 Alan Zimmerman <br />
Used by permission by Portland Code School
