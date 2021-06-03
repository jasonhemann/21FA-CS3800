---
title: Syllabus
layout: single
toc: true
toc_label: "Syllabus Contents"
---

### Collaborative Course Construction and Feedback 

We are together in unprecedented times. The typical course structure
implicitly assumes regular whole-class in-person meetings. As has been
the case for the last several semesters, we will not have that this
semester. No student will be physically present in class on all
days. Some students may not be physically present in class at all, or
on campus period. This change affects much of the course
infrastructure. As such, I *want* you all's feedback and input. I am
open to suggestions and changes; I consider this document preliminary
until the end of the first week of class. Even beyond that point I am
open to suggestions and changes by unanimous or near unanimous
consent. I cannot promise that we will act on all suggestions, and
even those we find compelling may not be implementable as we
go. Please do not hesitate. You can see any and all changes on the
course website's repository. Students in prior semesters gave a good
deal of feedback, and at times I wish they'd given more, and sooner.

## Purpose and Objectives

CS 2800 will introduce you to formal logic and its deep connections to
computing. The goal of the course is to introduce fundamental,
foundational methods for modeling, designing and reasoning about
computation. This course considers approaches to proving programs
properties including termination, correctness, and safety. The course
also introduces students to modeling with logic the range of artifacts
and phenomena that arise in computer and information science.

After this course you will know how to:

  1. translate statements about programs' behavior into logical claims
  2. prove such claims both by hand and via automated tools.

After this course you will appreciate the benefits thinking logically
when developing software, as well as the benefit of formal tools for
ensuring software correctness. You will also familiarize yourself with

  - propositional and first order predicate logic
  - logical inference
  - mathematical and structural induction
  - recursion 
  - equational reasoning,
  - rewriting, and 
  - various proof techniques

as well as the common notations for the preceding. We will study logic
from a computational perspective using the [ACL2 Sedan theorem proving
system](http://acl2s.ccs.neu.edu/acl2s/doc). **Please do not use the
installation instructions on the this website. Instead follow the
first lab assignment.**

## Contact

The best way to get in contact for personal, private (FERPA, etc)
messages is via my email address
[jhemann@northeastern.edu](mailto:jhemann@northeastern.edu). You
should expect a response within 48 hours. You will find that I am
faster with [Piazza]({{ site.baseurl }}/tech/) or our public forums. If I deem it even
potentially useful to others, I will likely anonymize your letter,
re-post it on Piazza, answer it there, and forward you the link.

A great regular way to reach out for help is via our [office
hours]({{ site.baseurl }}/office-hours/).

## Recent Changes

This semester I split the difference between exam-based summative
assessments that are more traditional in this course with
project-based ["authentic
assessments"](https://learning.northeastern.edu/event/workshop-using-projects-and-presentations-as-assessment-strategies-in-nuflex/). These
projects will be uniquely tailored with and for the particular group
of students, and may take the forms of proofs for topics that have
come up in practice or programmatic reduction of a real world example.

I'm also planning to use some of the last part of the course, while
students are working on these larger projects, to talk about
computational logic in a different context: logic programming. We can
also get into the "guts" of an implementation of such a system, where
ACL2, ACL2s is so much more sophisticated that it's tough for students
to wrap their heads around an implementation. 

If in fact you're interested in PL research, logic, logic program,
automated theorem proving or the like, please let me know on that too!
[I'm excited to talk more about it all
:-)](https://scholar.google.com/citations?user=SePR8OkAAAAJ)

## Required Texts 

There are no required texts for this course. Our course will follow a
draft of [Pete Manolios's](https://www.ccs.neu.edu/~pete/) [/Reasoning
About Programs/ (2021)]({{ site.baseurl }}/readings/). You will find these
notes linked from this website. I invite you to collaboratively
annotate these notes with me, and with each other.

## Technology and Platforms

As a course and a student body, we are more remote than usual, and
preferable. We will leverage a number of Northeastern's technology
platforms to help bridge the chasm. Your first lab assignment will
walk you through installing and configuring these.

We will use a variety of tools and platforms to facilitate teaching
and learning at a somewhat remote distance and to compensate for this
unconventional semester. These include but are not limited to ACL2s,
Eclipse, VirtualBox, CodeTogether, WaitWhile, PollEverywhere, and
Hypothes.is. Please see the [technology page]({{ site.baseurl
}}/tech/) for more details.

## Grade Breakdown

I will assign overall course grades as follows:

     | Category                  | Weight (%) |
     |---------------------------+------------|
     | Participation             |         15 |
     | Homework                  |         40 |
	 | Midterm Exam              |         15 |
     | Project Proposal          |          5 |
	 | Project Progress Report   |         10 |
     | Project, Presentation     |         15 |
     | TRACE evaluation          |          2 |
     | Total                     |        102 |

I will calculate overall numeric grade according to this grading
scheme. Everyone who gets at least 90% will get some form of A,
everyone with at least 80% will get at least some form of B, and
everyone with at least 70% will get at least some form of
C. Additionally, there will be a "curve", but I will determine it only
at the end of the semester. This curve will potentially raise grades
above those described here, but will not lower them. Therefore, the
total grade shown on Canvas does not necessarily reflects the
worst-case scenario of the letter grade you will get at the end of the
semester. This means I *cannot* give you a more precise estimate of
your grade than what you calculate from the raw score. I detail below
the aforementioned individual components of your final grade.

### Total Running Grade Calculation

We will track the completion portions of your lab and homework grades,
as well as your project grades, in
[Canvas](https://canvas.northeastern.edu/). You will have an
approximate assessment of your *current* grade status before the
Add/Drop deadline. We cannot give you a standing completion percentage
of the participation component of your grade because, logically, there
[are no pop
quizzes](https://en.wikipedia.org/wiki/Unexpected_hanging_paradox).

### Combined Lecture and Lab Grade

You have enrolled in both CS2800 and a section of CS2801, the
corresponding lab course. Both are components of this course grade and
tightly interwoven with each other. As a consequence I will be
assigning you a single grade across 

## Midterm Exam 

We will have one midterm exam. I have yet to determine its format, and
I am actively soliciting your input and advice as to what format this
should take. If you have strong preferences, suggestions, or
experience with exam formats that worked particularly well in this
hybrid class modality, please do make suggestions.

We will not have a final exam. Instead, our course will have a [final
project](Projects) component. During finals week, we will schedule
slots for [groups](Teamwork_and_Collaboration) of students to present
their final projects.

<!-- ### Alternate/Additional Assignment/Project Option -->

<!-- Throughout the semester there may be multiple opportunities for extra -->
<!-- credit. I want to give students an opportunity to demonstrate mastery -->
<!-- of the material in a way that resonates with you. If you feel like you -->
<!-- need or want more, or that your current assessments haven't -->
<!-- sufficiently demonstrated your understanding, please speak with -->
<!-- me. Under many exceptional circumstances we can come up with -->
<!-- additional or side-projects for the students to demonstrate mastery of -->
<!-- the material in class and then some. *Warning:* these will likely be -->
<!-- larger term assignments and you should not consider this an even -->
<!-- substitute. Certainly not the easy way to receive full marks. But a -->
<!-- way to redistribute some portion of the grade.  -->

## Participation

I expect you to attend lecture and lab each class period. Your
attendance is a prerequisite for a substantial portion of the course's
grade, both in your lecture and lab sections. We will [not take
attendance](https://vm.tiktok.com/ZMJBoQovg/) as such, but attendance
is a prerequisite for participation. We will have reading content
quizzes and elicit oral or group explanations as proxies for
participation. 

### Content Quiz, Pre-reading

Before class, I will expect you to have read the notes as marked on
the schedule. These act as a forcing function for the lecture notes
and alert me to students' difficulties. Sometimes we take these for
completion, others for accuracy. These lecture quizzes belongs under
your participation grade.


### Oral Explanation and Participation

Proof has a [social
component](https://www.jstor.org/stable/3482651). As such, part of
your grade will also include your participating by communicating with
your colleagues in both lecture and lab sections. These can take the
form of small group "breakout room" work, open class votes and
discussions, or walk us all through some of your answers. 

#### Recording 

I do not permit electronic video and/or audio recording of class in
either modality. Unless the student obtains permission from the
instructor electronic video and/or audio recording of class is
prohibited. If permission is granted, any distribution of the
recording is prohibited. Students with specific electronic recording
accommodations authorized by the [DRC](academic-accommodations) do not
require instructor permission; however, the instructor must be
notified of any such accommodation prior to recording. Any
distribution of such recordings is prohibited. Obviously I cannot
[stop you](https://obsproject.com/), but it's to both our benefits.

## Homework 

In order to better scaffold your homework assignments and in order to
let us help you better, I have divided homework assignments in
half. Unless otherwise stated, I will release your homework
assignments on Monday evenings. You will have the opportunity in lab
to discuss and go over questions on the first half of these
assignments, giving you both more incentive to get a jump start and
also opportunities to check your understanding.

### Submissions

For a homework released on Monday, the first half is due Saturday at
1pm, and the second half due the following Wednesday at 10pm (again
unless otherwise indicated). Unless otherwise indicated, you will
submit your homework on Gradescope. You will work on homework in your
chosen [group](Teamwork_and_Collaboration).

### Late / Mistaken Assignment Policy

To universally, uniformly and preemptively account for any number of
situations that arise, *I will drop every student's lowest three
half-homework assignment grades. This is effectively one and a half
homeworks.* This absolution for one and a half of our assignments _is_
our late/etc homework clemency. Please do consider what this does
mathematically for your overall final grade.

The final two homeworks, will both be one-part, and worth half the
usual homework weight. Since they're worth half the usual homework
weight, I'll also count that as dropping a "half an assignment"
rather than a full one, because it's worth half the others.


I shan't accept late submissions except under the most exceptional of
circumstances (family emergencies, hospitalizations, the like)---if
that comes up please see me.

## Projects 

I suggest roughly two areas of focus for your projects in this
course. Together with your partner/mob, you should start thinking
about what you might want to do. One likely option is something
related to SAT/SMT solving, likely a reduction of some
existing-but-unsolved problem to SAT in a way that produces
answers. The other style is a formal mechanized proof of some small,
real-world example worth proving. These might be something from
Fundies I, Fundies II, from your math classes, or somewhere else from
your own experience. These should be large enough to be of interest,
so that ACL2 cannot automate it for you, but not thesis-level
challenging. The proof should be in some way enlightening, and your
presentation and accompanying documentation will exhibit this.

I will release the project guidelines approximately one month before
its due date. When I do so you will have also a timeline outlining
your due dates for each stage. You should expect the following stages:

  - Roughly four days to one week after I've assigned your project,
    your group will meet virtually with me or one of several
    designated TAs to discuss your project idea and get clearance to
    proceed.
	
  - Roughly two weeks before its due date, you will submit to me a
    progress report with source code and your status at this point. 
	
  - Roughly two to four days before the due date, you will have
    submitted to me a "receipt" for either having checked out from the
    library one of several well-known and trusted [style
    guides](https://subjectguides.lib.neu.edu/c.php?g=713111&p=5073143#s-lg-box-wrapper-18808483)
    or for having had an
    [appointment](https://cssh.northeastern.edu/writingcenter/tutoring/online-appointments/)
    at the writing center where you have copy-edited your draft. They
    have a [whole bevy of resources for you]({{ site.baseurl
    }}/faq/improve-writing/). Please note I am asking you to do more
    than an elementary grammar check and appropriate citations, I want
    you to thoroughly copy-edit your prose before submitting.

  - Roughly a month after I've assigned your project, your group will
    submit to me via a dropbox your project report, as follows:
	  1. A stand-alone PDF document that contains a link to a source
         repository that I can access. 
      2. This repository must contain and your source code, with
         suitable instructions for me to build and run your
         deliverable.

  - Roughly a 28 to 34 days after I've assigned your project, your
    group will meet with me virtually to discuss and demonstrate your
    project and results.

## TRACE evaluations

I encourage students to take time and submit TRACE evaluations. Your
time is busy at the end of the term when these are available. In order
to fairly compensate you for that time, if 85% or more of the students
enrolled in a section complete these TRACE evaluations, then I shall
add two points onto the class-wide final average.

## Academic Integrity Policy

Students of course play an integral part in ensuring they receive the
full benefit of their coursework. The students of 2800 are certainly
beholden to the academic integrity policies of [Northeastern
University](http://www.northeastern.edu/osccr/academic-integrity-policy/),
the [Khoury
College](https://www.khoury.northeastern.edu/information-for-overview/current-undergrad/undergraduate-advising-academic-support/academic-policies/).

### Teamwork and Collaboration

I had originally stipulated that groups of at least 2 from within the
same lab section. *Gradescope cannot enforce either, so I will not
require them.* You can work with up to 3 others, for a total of 4
people in a group. You aren't required to work with anyone else if you
don't wish. You can work with students from any other sections you
wish. You will submit a single submission for your entire group, and
it is your responsibility to include the names of your group members.

Do bear in mind pair programming is a central part of the
undergraduate curriculum here. Pair programming is not intended to
divide-and-conquer, but instead for students to collaboratively solve
problems together. You are only twice as fast working separately if
the typing is by and away the hardest part of programming. Which it is
not.

Whatever size group you work in you should still plan to [all work
synchronously and simultaneously
together](https://www.remotemobprogramming.org/). Note a larger group
is not necessarily better. You should at least try to do some of this
wholly on your own. It's good to have a baseline early on to know [if
you have this material under your belt or if you are getting
lost](https://martinfowler.com/articles/on-pair-programming.html#couldIReallyDoThisByMyself). Ultimately,
you should be responsible for and have a firm understanding of all
work submitted under your name. You should be able to demonstrate this
mastery when we request.

#### Group Dynamics and Difficulties

If you find that your group is no longer able to work effectively
together or that not everyone can equally participate, please bring
this to your lab instructor's attention. Your lab instructor may have
suggestions about how to improve your group cohesion, or may use the
staff privilege to reallocate group members. 

## Academic Accommodations 

If you have accommodations from the [Disability Resource Center
(DRC)](http://www.northeastern.edu/drc/) please submit your Professor
Notification Letter to me by email, preferably within the first two
weeks of the quarter, so I can do my part to help you achieve equal
access in this course. I am eager to discuss ways we can ensure your
full participation.

I encourage all students who may benefit from learning more about DRC
services to [contact the
DRC](http://www.northeastern.edu/drc/#fp-blog-entry:~:text=Contact%20Information).

## Health and Safety

The university has put into place a robust plan to make the campus
healthy and safe for all — but you must do your part. On August 22, all
students received an
[email](https://news.northeastern.edu/coronavirus/university-messages/university-response-to-unsafe-behavior/)
from Senior Vice Chancellor for Student Affairs Madeleine Estabrook on
the expectations for behavior both on campus and off campus. **Please
read it carefully today.**

To summarize:

* Gatherings on or off campus must conform to healthy practices as
  outlined by university and [Massachusetts state
  guidance](https://www.mass.gov/doc/revised-gatherings-order-august-7-2021).
  If you host or attend an inappropriate party or gathering, you run the
  very real risk of immediate removal from the community.

* Wear a mask indoors and outdoors as you maintain a 6-foot distance
  from everyone.

* Get tested every three days using the COVID-19 Test Scheduler
  ([covid19-testing.northeastern.edu](https://northeastern.sharepoint.com/sites/covidscheduler).)
  We may require more frequent testing as the semester progresses. It’s
  quick, easy and will help us to quickly identify and care for anyone
  who tests positive. I will not be told the identity of anyone who
  tests positive, and you do not need to share that information with me
  or anyone else unless you want to. If you receive a positive test
  result, you will be contacted by a member of the university’s
  telehealth team who will provide you with next steps.

* Do a Daily Wellness Check
  ([wellness-check.northeastern.edu](https://wellness-check.northeastern.edu)),
  wash your hands well and regularly, and disinfect high-touch surfaces
  and spaces.

* I will be wearing a [face
  covering](https://news.northeastern.edu/coronavirus/reopening/frequently-asked-questions/#reopening)
  or mask as I teach and expect that you will do the same in class. If
  you come to class without a mask, I’ll ask you to go and [get one on
  campus](https://news.northeastern.edu/coronavirus/reopening/policies-and-protocols/#face-covering-protocol).
  You can get a mask at the Visitor Center or at the Curry Student
  Center Help Desk. If you refuse to wear a mask in class, I won’t be
  able to continue the class. If you are not sitting six feet apart from
  your classmate, I’ll ask you to do so. We won’t be able to eat or
  drink in class (except water). If you test positive, you will need to
  enter isolation as directed by the university’s telehealth team. I
  expect that you will not come in-person to class and that you will
  follow the guidance from the university telehealth team to isolate and
  get appropriate healthcare if needed.

* Staying safe is a responsibility that we all must take seriously.
  Keep in mind the “Protect the Pack” theme. Remember that our
  individual actions will help everyone stay safe this fall."

## Equity and Compliance

One of our responsibilities in supporting student learning 360° is to
help create a safe learning environment both in person and
virtually. You should carefully consult the university's [relevant
policies](https://www.northeastern.edu/ouec/title-ix-policy-2/), and
if you have or experience any violations of the above I encourage you
to take full advantage of the [university
resources](https://www.northeastern.edu/ouec/resources/main-campus-resources/).

It is also important that you know that federal regulations and
University policy require me to promptly convey any information about
certain kinds of misconduct known to me to our Deputy Title IX
Coordinator or IU’s Title IX Coordinator. In that event, they will
work with a small number of others on campus to ensure that
appropriate measures are taken and resources are made available to the
student who may have been harmed. Protecting a student’s privacy is of
utmost concern, and all involved will only share information with
those that need to know to ensure the University can respond and
assist.

## Acknowledgments 

Pete Manolios is responsible for much of our course infrastructure and
assignments. Pete Manolios and [Stavros
Tripakis](https://www.ccs.neu.edu/~stavros/) inspired some the lecture
contents and topics, and in some cases designed the slides. [Lindsey
Kuper](https://users.soe.ucsc.edu/~lkuper/) inspires some of this site
as well as being all-around inspirational. Suzanne Menzel also
inspires some of this syllabus language.

![In the syllabus]({{ site.baseurl }}/assets/images/syllabus.gif "Might just be worth checking.")


