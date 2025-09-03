- [CS 1632 - Software Testing](#cs-1632---software-testing)
  * [Description](#description)
  * [Rent-A-Cat System](#rent-a-cat-system)
  * [Create a Test Plan and a Traceability Matrix](#create-a-test-plan-and-a-traceability-matrix)
  * [Report Defects](#report-defects)
  * [Format](#format)
  * [Grading](#grading)
  * [Submission](#submission)
  * [Groupwork Plan](#groupwork-plan)

# CS 1632 - Software Testing
Fall Semester 2025

* DUE: September 24 (Wednesday), 2025 before start of class

**GitHub Classroom Link:** TBD

This is going to be your first group assignment.  When you click on the GitHub
Classroom link, you will be asked to either create a new team or join an
existing team.  Please use the team name that you listed on the Partnership
Contract.  If your partner already created a team, join that team rather than
create a new one.

## Description

The parameters of this assignment are identical to that of [Exercise
1](../../exercises/1).  Please review the Exercise 1 README carefully as well
as the feedback you received from your submission, if there was any.

Just like for Exercise 1, you will create a test plan with associated
traceability matrix and then find, report, and route at least three defects
through the GitHub issues system.  Just like for the exercise, you are asked to
cover all program behaviors using your knowledge of equivalence classes, and
also include at least one edge case and one corner case as part of your testing
in addition to base cases.

## Rent-A-Cat System

We are going to be testing the Rent-A-Cat system for the deliverable.
Rent-A-Cat rents cats to customers for various needs (mousing, companionship,
homework help, etc.).  From the main menu, users may:

1. See list of cats for rent
2. Rent a cat to a customer
3. Return a cat
4. Rename a cat
5. Quit

A cat which is out for rental cannot be rented and will not be listed until it
has been returned.  A cat that is unavailable cannot be renamed either until it
hass been returned.

You can run it using the rentacat.jar file included in the repository:
```
java -jar rentacat.jar
```

Try playing around with the app a little bit to get a feel of it.

## Create a Test Plan and a Traceability Matrix

Create a test plan and traceability matrix based on The requirements listed in
the file [requirements.md](requirements.md).  

**Please apply everything you learned in Exercise 1 here.  Also, please try to
avoid any of the pitfalls I discussed in the recorded lecture.**

Now, there are a couple of things in the deliverable that you have to watch out
for beyond what you did for the exercise.  They all stem from the fact that
running Rent-A-Cat may involve a prolonged interaction between the program and
the user.  

1. PRECONDITIONS: You may be tempted to set as the precondition some state
   after a prolonged interaction with the program.  For example in Rent-A-Cat,
when testing FUN-2-RENT-COMMAND , the outcome of the rent command will differ depending
on the availability of cats at that point.  So you may be tempted to set as a
precondition "Cat ID 1 is rented out", or "Cat ID 1 is available", depending on
what you want to test.  This can cause problems with reproducibility.

   Suppose the precondition is "Cat ID 1 is rented out".  There are a zillion
ways in which the player could have ended up in that state.  The player could
have rented out and returned cat any number of times previously.  And, maybe
that history matters... who knows?  Also that precondition does not mention
anything about the state of other cats.  In theory, it should not matter, but
who knows?  Therefore, per the discussion in the test plans lecture, whenever the
preconditions include some internal program state of the system under test,
that state is more reliably reproduced if instead those preconditions are
expressed in terms of execution steps that achieve that state.  So, instead of
the following:

   ```
   PRECONDITIONS:
   - Cat ID 1 is rented out.
   ...

   EXECUTION STEPS:
     1. Type "2[Enter]" at prompt for command.
     2. Type "1[Enter]" at prompt for cat ID.
   ```

   The following is far superior in terms of reproducibility:

   ```
   PRECONDITIONS:
   - All the requisite preconditions for running the app.
     ...

   EXECUTION STEPS:
     1. Launch the app by typing "java -jar rentacat.jar[Enter]" on the commandline.
     ... steps required to rent out cat ID 1...
     4. Type "2[Enter]" at prompt for command.
     5. Type "1[Enter]" at prompt for cat ID.
   ```

2. POSTCONDITIONS: A postcondition is a condition that needs to be in place
   **after** having performed the execution steps (hence the prefix "post").
Now, if you have many execution steps as part of a prolonged interaction, you
may be tempted to check a condition mid-way through the steps (let's call these
"mid-conditions").  In effect, you would be checking multiple things throughout
the steps of a single test case.  This is a clear sign that you are trying to
merge multiple test cases into a single test case.  If you take this to the
extreme, you may end up with just a single jumbo test case that tests
everything about your program in one shot!  This is no way to test your
program.  If that jumbo test case fails, then it is unclear which part of your
program failed and what requirement is not working (compared to many discrete
test cases).  Also, if that jumbo test case fails somewhere in the middle, that
means you will not be testing things later on in the test case, which creates
artificial dependencies between test scenarios.  We learned the importance of
independence when creating test cases in the lecture.  A test case should test
one behavior at a time and all the preconditions and execution steps should all
be preparation to test that one behavior.

## Report Defects

Report at least 3 defects found using the test plan.

**Again, please apply everything you learned in Exercise 1 here.**

For each defect, open a GitHub issue, triage the issue, create a branch,
resolve the issue through requirement modification, create a pull request, and
close the issue by pulling the branch, just like we did for Exercise 1.

## Format

The report should start with a cover page with:
* The names of the people in the group

Write a short introduction that includes:
* How you divided the work between members of the group.
* IDENTIFIER of one base case and why you think it is a base case.
* IDENTIFIER of one edge case and why you think it is an edge case.
* IDENTIFIER of one corner case and why you think it is a corner case.

When you think of edge cases, remember that objects (even rooms!) can be values
as well as numbers and strings.

ON A NEW PAGE, a traceability matrix should be provided mapping the test cases
with their associated requirements.  Remember that all requirements should map
to AT LEAST ONE test case, and all test cases should map to AT LEAST ONE
requirement.  

ON A NEW PAGE, a list of the actual test cases should follow.  You may name
them any way you wish, but please be consistent.  Please write them out in this
format -

	IDENTIFIER:
	TEST CASE:
	PRECONDITIONS:
	EXECUTION STEPS:
	POSTCONDITIONS:

ON A NEW PAGE, copy and paste the link to your GitHub repository issues page
with the 3 closed issues.

## Grading

* Introduction: 20% of grade
* Traceability Matrix: 15% of grade
* Equivalence Class Coverage: 15% of grade
* Test Plan: 20% of grade
* Defects Reporting: 30% of grade

Please review the [grading_rubric.txt](grading_rubric.txt) for details.

## Submission

Please use the [ReportTemplate.docx](ReportTemplate.docx) file provided in this
directory to write your report.  If you don't have a .docx compatible word
processor, that's perfectly fine as long as you follow the same organization.
A PDF version of the file is at [ReportTemplate.pdf](ReportTemplate.pdf).
Please make sure that the intro, traceability matrix, test cases, and defects
are on seperate pages.  You will be submitting to GradeScope in PDF format.
When you submit, you will be asked to assign pages in the PDF file to each
rubric item: 1. Introduction, 2.  Traceability Matrix, 3. Equivalence Class
Coverage, 4. Test Cases, and 5. Defects.

Each pairwise group will do a shared submission to the **Deliverable 1**
GradeScope link.  Make sure that your partner is added by clicking on the "View
or edit group" link on the top right of the submission, or he/she/they will not
get a grade!

## Groupwork Plan

I suggest that you create a shared document that both of you can work on using
Google Docs or Microsoft OneDrive or your preferred cloud service.  Divide the
requirements up between the two of you in a sensible way.  Once you are done,
check each other's work, discuss, and submit!  In order to leave time for
discussion, I strong suggest you complete the work at least 2 days before the
deadline.
