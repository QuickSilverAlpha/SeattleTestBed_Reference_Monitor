# SeattleTestBed_Reference_Monitor
Educational Assignment

## Part 1: Implement a Defensive Security System

This assignment will help you understand security mechanisms. You will be
guided through the steps of creating a reference monitor using the security
layer functionality in Repy V2. A reference monitor is an access control
concept that refers to an abstract machine that mediates all access to
objects by subjects. This can be used to allow, deny, or change the
behavior of any set of calls. While not a perfect way of validating your
reference monitor, it is useful to create test cases to see whether your
security layer will work as expected (the test cases may be turned in as
part of the next assignment). 

This assignment is intended to reinforce concepts about access control and
reference monitors in a hands-on manner. 




### Overview
----
In this assignment you will create a security layer which will always left indent 
after the '\n' newline character in a write that strictly appends to a file.   By 
"strictly appends", this means the first byte of the write is at the current end 
of file (after the last previously written data).  This is something that is 
sometimes done by a document editors, when they believe you have ended a paragraph.  
For this assignment, the '\n' character is treated as a newline and other characters 
(notably '\r') are not treated specially.

You should write test applications to ensure your reference monitor behaves properly 
in different cases and to test attacks against your monitor.    

#### The Reference Monitor Must:
1. Behave identically to a non-sandboxed program [RepyV2 API calls](../Programming/RepyV2API.md) for
   all calls other than a writeat()s that strictly append.  So other writeat()s, readat()s, etc. 
        must be performed as they would in a non-sandboxed program!
2. If a writeat() strictly appends to a file, then:
   * If it contains no '\n' characters, perform the writeat() operation normally (as a non-sandboxed program)
   * If it contains exactly one '\n' character, then perform a writeat() that strictly appends, 
     but with four space ' ' characters inserted after the '\n'.   
   * If it contains more than one '\n' character, raise a RepyArgumentError exception
3. Not produce any errors or output for any reason except as mentioned above  
   * Normal operations should not be blocked or produce any output  
   * Invalid operations should not produce any output to the user
4. Not call readat() everytime writeat() is called.  This will be too slow and is forbidden.


Three design paradigms are at work in this assignment: accuracy,
efficiency, and security.

 * Accuracy: The security layer should only modify certain operations (a strictly
appending writeat() with one '\n') and raise an exception for certain other 
actions (a strictly appending writeat() with more than one '\n'). All situations 
that are not described above *must* match that of the underlying API.

 * Efficiency: The security layer should use a minimum number of resources,
so performance is not compromised.  For example, you may not call readat() 
everytime writeat() is called.  It is permissable to call readat() upon fileopen(),
however.

 * Security: The attacker should not be able to circumvent the security
layer. For example, if the attacker can cause a non-strictly appending write to
have '    ' inserted after '\n' or can cause the reference monitor to incorrectly
error or hang, then the security is compromised.


# Part 2: Security layer testing and penetration

In this assignment you will learn how to attack a reference monitor. The reference monitor you will be testing uses the security layer framework (encasement library, etc.) for the Seattle testbed. It is possible to do this assignment separately, but it is recommended that this assignment be completed after [Part One](LeftPadPartOne.md). Either way you should already have a working security layer or access to one. Testing the security layer is done by running a series of test cases that an adversary may use to circumvent your system. This assignment is intended to prepare you for thinking about security paradigms in a functional way. The ideas of information, security and privacy have been embedded into the steps of this assignment.


### Overview
----
In this assignment you are a tester. You have been sent a bunch of reference monitors that need testing before they are deployed. Your job will be to ensure an attacker cannot circumvent these security layers. In order to do this, you will attempt to write, and append invalid data. If you are able to do so, then the security layer is not secure. The future of the system depends on your ability to test code thoroughly!   

Three design paradigms are at work in this assignment: accuracy, efficiency, and security.

 * Accuracy: The security layer should only stop certain actions from being blocked. All other actions should be allowed.

 * Efficiency: The security layer should use a minimum number of resources, so performance is not compromised.

 * Security: The attacker should not be able to circumvent the security layer.

Within the context of this assignment these design paradigms translate to:

 * Accuracy:  The security layer should only modify certain operations (a strictly appending writeat() with one '\n') and raise an exception for certain other actions (a strictly appending writeat() with more than one '\n'). All situations that are not described above must match that of the underlying API.

 * Efficiency: The security layer should use a minimum number of resources, so performance is not compromised. For example, you may not call readat() everytime writeat() is called. It is permissible to call readat() upon fileopen(), however.

 * Security: The attacker should not be able to circumvent the security layer. For example, if the attacker can cause a non-strictly appending write to have ' ' inserted after '\n' or can cause the reference monitor to incorrectly error or hang, then the security is compromised.

You will submit a zip file containing all of the tests you have created. You will gain points for every student's reference monitor you find a flaw in. It is good if multiple tests of yours break a student's reference monitor, but you gain the same number of tests whether one or more tests break the layer.


#### Prerequisites

This assignment assumes you have both the latest Python 2.7 and RepyV2
installed on your computer. Please refer to the [SeattleTestbed Build Instructions](../Contributing/BuildInstructions.md#prerequisites)
for information on how to get them.
