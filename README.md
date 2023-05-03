Download Link: https://assignmentchef.com/product/solved-cs3210-project-1-mal-syntax-checking
<br>



<ul>

 <li>added preliminary design, under other specification details</li>

 <li>removed “not collecting design” under development notes</li>

 <li>added to incremental testing under development notes</li>

 <li>deadlines: added initial schedule and design (with language) posted to Moodle before next class</li>

</ul>

<u>Project Description</u>

The program takes a MAL (minimal assembly language) program, and runs the first steps of a preprocessor / translator (assembler): removing comments and checking for syntax errors.  Your program processes the code, and creates a report file with error messages (if any) and a comments-removed listing of the code.

<u>Project Specifications</u>

Errors detected:

<ol>

 <li>ill-formed label: the first token ends in a colon but doesn’t follow the rules for a label name</li>

 <li>invalid opcode: the first token is not one of the valid opcodes

  <ol>

   <li>special case: if the line contains a label, then the opcode should be the second token</li>

  </ol></li>

 <li>too many operands: for the specific opcode, there are more operands than required</li>

 <li>too few operands: for the specific opcode, there are fewer operands than required</li>

 <li>ill-formed identifier: an identifier is invalid (non-letters or more than five letters)</li>

 <li>ill-formed literal: a numeric literal is invalid for octal</li>

</ol>

Warnings: labels

<ol start="7">

 <li>a branch goes to a non-existent label</li>

 <li>a label is never branched to</li>

</ol>

Other details

<ol>

 <li>See the separate sheet for the syntax of the Mini Assembly Language (MAL).</li>

 <li>High-level design of your main program:</li>

</ol>

<ul>

 <li>read in MAL program</li>

 <li>output original program with line numbers to report file</li>

 <li>strip comments and blank lines</li>

 <li>output stripped program with line numbers to report file</li>

 <li>for each MAL program line …</li>

</ul>

… write numbered line to report file

… check errors (in the order above), stopping after first error

… write error message (if any) to report file

<ul>

 <li>write summary data to report file</li>

</ul>

Preliminary design: list all functions needed (individual tasks) and primary data structures.

<ol start="3">

 <li>Your program takes a file name as an argument, and appends the extension <em>.mal</em>, then uses that as the input program file name.  This file contains (what is supposed to be) a program written in MAL, in plain text form.  You may assume that the incoming string follows file name syntax, and that the file exists, is in the right folder, can be opened and read, and is non-empty.</li>

 <li>Detection of an error on a line halts processing on that line (don’t scan for further errors).</li>

 <li>Make your error messages helpful and informative – remember the bad messages you have had to deal with as a programmer! Suggest corrections where it’s easy.  Easy example: “too many operands – expected 2 operands for ADD”.  Hard example: “invalid opcode SBB – should be SUB?”.</li>

 <li>You do not need a character-by-character lexical analyzer or tokens. Just use standard input string parsing (possibly built into your language) and string routines (but nothing that trivializes the main thrust of this assignment; if in doubt, ask me first).  Use lots of little work routines (e.g., is-valid-id, process-add-op, is-octal-num).</li>

 <li>Report file. Your program creates a report file in the same directory as the original (input) program.  Its name is the same, minus the extension <em>.mal</em>, and with the extension <em>.log</em></li>

 <li>Limitations / what the program does not do.

  <ol>

   <li>check or correct style</li>

   <li>check semantics (does the program make sense?)</li>

   <li>translate to machine code</li>

  </ol></li>

</ol>







Report file format: heading, three versions of the source code, summary

<ol>

 <li>heading: some nice title, MAL file name input to the program, report file name, process date (use the system date), your name, CS 3210</li>

 <li>code, three versions, labeled

  <ol>

   <li>original version: line-by-line listing of original source code with numbered lines</li>

   <li>“stripped” version: line-by-line listing of source code with comments and blank lines removed

    <ol>

     <li>lines retain their original formatting</li>

     <li>lines are numbered as they were in the original file</li>

    </ol></li>

   <li>error report version: line-by-line listing of source code (blank lines and comments removed) with error messages (if any) shown below their line of code; note that if there are no errors this will exactly match version two</li>

  </ol></li>

 <li>summary

  <ol>

   <li>ending totals: number of lines of actual code (not blanks and not comment-only lines), number of errors found (do not show error categories with no errors), and total error count</li>

   <li>final statement: <u>MAL program is / is not valid</u></li>

  </ol></li>

</ol>

Sample partial report file (next page).  Notice the three different versions of the MAL program: original, stripped (no blank lines or comments), and annotated with error messages.  “Bad” formatting has not been normalized.  Also notice, on line #4, no checking could be done on the operand list; and on line #9, only the first error is reported.  Finally, there are no lines numbered 4, 5, or 7, which means those lines in the original file were either blank or had only a comment.  Follow this report format.

&lt;report file heading as given above&gt;




————-

original MAL program listing:

<ol>

 <li>; multiple errors, author: J. Gurka</li>

 <li>LOAD         R5, X</li>

 <li>ADD                       r2,r7,r7</li>

 <li>SBB   R4, R5, total ; error:  should be SUB</li>

 <li></li>

 <li>  ;;;   comment-only line</li>

 <li>STORE      total, R9          ; flipped operands</li>

</ol>

8.

<ol start="9">

 <li>ADD                       123go  ; too few operands and bad identifier</li>

 <li>END</li>

</ol>




————-

stripped MAL program listing:




<ol start="2">

 <li>LOAD         R5, X</li>

 <li>ADD                       r2,r7,r7</li>

 <li>SBB   R4, R5, total</li>

 <li>STORE      total, R9</li>

 <li>ADD                       123go</li>

 <li>END</li>

</ol>




————-




error report listing:




<ol start="2">

 <li>LOAD         R5, X</li>

 <li>ADD                       r2,r7,r7</li>

 <li>SBB   R4, R5, total</li>

</ol>

** error: invalid opcode SBB

<ol start="7">

 <li>STORE      total, R9</li>

</ol>

** error: ill-formed operand, expected register, found identifier: total

<ol start="9">

 <li>ADD                       123go</li>

</ol>

** error: too few operands for ADD, expected 3 operands

<ol start="10">

 <li>END</li>

</ol>




————-




total errors = 3

1  invalid opcode

1  too few operands

1  ill-formed operand

Processing complete – MAL program is not valid.

<h1>Development Notes</h1>

<ol>

 <li>You may use any language for this project.  Email me with your language choice within a couple days.  If you use C++, your program should be fully object-oriented (use C if you don’t want OO).  Do not use any tools such as lex, regular expressions, or tokenizers that do the bulk of the work for you – you should be explicitly doing the parsing in your code.  Also don’t use built-in exception handling – do error trapping yourself.</li>

 <li>Create a detailed project schedule and try to stick to it.  Plan to finish each component two days early to allow for any problems.</li>

 <li>Cover letter. Use the cover letter template on Moodle.  Make notes for your cover letter as you work.  Your final notes to me should be thorough and not written at the last minute – more specifications below.</li>

 <li>I have given you the bare-bones design.  The remaining non-trivial design is the logic for checking each error.  <span style="text-decoration: line-through;">Since you’ll be developing this as you go along, I will not be collecting a separate design</span>, but please think before you code – I guarantee this will save time!  I will ask you a couple times during the assignment what you have finished, what’s in progress, what’s not started, and what problems you are having or have had.  Be prepared to send this information at any point.</li>

 <li>Develop your code modularly.

  <ol>

   <li>First, get a running, stubbed program, in order to fully organize program flow and functions.</li>

   <li>Then have the program simply produce a report file, without removing comments or blank lines, and without error checking. I will post two different MAL programs on the MAL forum, to use as initial test cases; they will not have blank lines, or comments, or errors.</li>

   <li>Next add processing for blank lines and comments; you should get error reports because they have no errors (and because you are not doing any error checks …).</li>

   <li>Then add one error check at a time.</li>

  </ol></li>

 <li>Testing, incremental. Test each logic addition as you go, by introducing blank lines, then each type of comment, then each error type into either one of the MAL plain test programs I provided.  For each error, first try a MAL program that has only that error, in several places and guises. The Moodle forum for test programs will have two programs for each error, written by classmates.  These programs will have only that error type, plus a beginning comment with the student’s name and the error type.  See the examples on the forum.  Then try running against MAL code with all previous errors plus the new one (regression testing).  Do not try to write code for all errors at once – it’s very likely to cost you more time (and frustration!) in the end.</li>

 <li>Testing, MAL programs. You will have multiple test programs to run, posted on the Moodle forum.  Test your program against all the MAL programs provided.

  <ol>

   <li>Two programs from me, basic, no errors, no comments, no blank lines.</li>

   <li>One program from you built from one of my programs (pick either one) that has test cases added for all errors, comments, and blank lines (added and tested one at a time).</li>

   <li>Multiple programs from classmates. Everyone will post two programs on the MAL programs forum.  One will have only one error type (as assigned in class), the other will be a general program with multiple errors, comments, and blank lines.</li>

  </ol></li>

 <li>Your final program should be well organized, well documented, modular, polished, etc. Produce a high-quality project that you would be happy to show a prospective employer.</li>

 <li>This is an individual project. Other than the first day discussions in class, do not work with classmates, or get help from buddies at work or home.  And this is not an assignment in see-what-you-can-find-on-Google.  Please do your own work.  Exception: once you have the basic project completed and working fine, you and a classmate may discuss and work on some of the extra credit – just mention your classmate in your cover letter.  Come to office hours any time for help, hints and ideas, code walk-throughs, chit-chat, etc.  Don’t get stuck making no progress for hours (or days!).</li>

 <li>Be sure to scrutinize your output at every step – are you getting what you should be getting?</li>

 <li>Deadlines and Deliverables:

  <ol>

   <li><u>before</u> handing anything in, please double-check these specs carefully! ask if you have any questions</li>

   <li>in class today: preliminary schedule for entire project post on Moodle before next class</li>

   <li>design: post on Moodle before next class</li>

   <li>language: email me your choice of language in the next day or two include with design</li>

   <li>Feb. 2, midnight: MAL programs (2) on Mal forum, one with several of one error type (assigned in class), one with many errors; include your name as a comment and the error type for the first program</li>

   <li>final project: Feb 27 (4 weeks) – post all these to Moodle; in addition, hand in a paper copy of your projects source code

    <ol>

     <li>final source code, meeting all specs, plus any extra credit</li>

     <li>output reports (2) from my (unaltered) initial MAL test programs</li>

    </ol></li>

  </ol></li>

</ol>

<ul>

 <li>your final 3 MAL testing programs, one with only one error type (already posted to the forum) one created from one of my originals during development, and one created from scratch by you (also posted on the forum); please highlight or mark all errors in your MAL programs (and each should have a comment associated with it); example:</li>

</ul>

;;;  calculate total

SUB Total, R3, R3              ; update total

ADDD          R1, R2             ; invalid opcode

<ol>

 <li>output reports from your three MAL programs</li>

 <li>any extra credit test MAL programs and report files</li>

 <li>final thorough cover letter (about 2 pages, use the template to be posted on Moodle), including:

  <ul>

   <li>your total time – keep track as you go, don’t guess or leave this out; nearest quarter hour is fine</li>

   <li>“how’d it go” discussion</li>

   <li>brief schedule discussion: was your initial schedule a fairly good plan? did you follow it? what you would change in general the next time you make a project schedule?</li>

   <li>a discussion of the ins and outs of the first pass of a preprocessor / translator across a program – what does it do? how does it do it? did you use multiple passes? did you need multiple passes – why or why not?</li>

   <li>a discussion of what errors testing found in your program, including whose test programs caught the errors</li>

   <li>a discussion of 3 errors or problems that were not checked (syntax or semantics) that could have been checked, and how hard it would be to add to your program</li>

   <li>a discussion of 3 error-checking issues did not arise using MAL, but that would be present in most high-level-language programs; discuss how they might be handled, and how that would add to the complexity of the translator</li>

  </ul></li>

</ol>