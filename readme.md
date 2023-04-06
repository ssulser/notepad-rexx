# Rexx Functionlist for Notepad++
Since I am looking into Rexx, I searched for good editors or IDE's on the internet. Unfortunately, the offer is sparse. But even the plugins for Visual Code Studio do not offer an automated function list.

I managed after a few tries to create a regex parser for Notepad++ that it suffices for my needs. The function list shows routines, procedures and the object-oriented terms of ooRexx (::class, ::method).

Of course there is still room for improvement. But since I'm far from being a regex pro, that should take some time.

##What does the parser recognize?

Source                      function list
------                      -------------

routine:              ->    routine
  nop
  return
  
proc: procedure       ->    proc

::class myClass       ->    myClass (as Class)
  ::method myMethod   ->    myMethod (as Method of Class)
  
###Defining the end of a class in the source code
Because of the way the parser works, the end of a class must be marked in the source code. Otherwise the parser will not work properly.

::class myClass
  ::method init
  ::method myMethod
-- myClass            -> -- is enough, but giving any further information may be helpful for readability

::class mySecondClass
  ::method init
-- mySecondClass


I have solved it in such a way that a class range of ::class goes up to the first occurrence of '--'. Therefore the C-style comments (/* .... */) must be used to comment within the class.
