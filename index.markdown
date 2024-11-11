---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

title: COMP394 - Natural Language Processing (Fall 2024)
author: Suhas Arehalli
category: Syllabus
layout: post
---

Welcome to the COMP394 (Natural Language Processing) Course Page. For course policies, please check the [syllabus](https://docs.google.com/document/d/1KVAYYU9B2DLcGQ_XvX9-6RNqVW7b_FI0NXx0UJjzXj4/edit?usp=sharing).


### Resources

#### Course Staff & Office Hours
##### Instructor:
Suhas Arehalli \\
Tu/Weds/Fri 2--3pm \\
OLRI 229

##### Preceptors:
Kien Nguyen \\
Mon 1--2pm, Th 4:30--6:30pm \\
Smail Gallery

#### Textbook
[Jurafsky & Martin, *Speech and Language Processing*](https://web.stanford.edu/~jurafsky/slp3/)

### Schedule
The schedule below will be updated to keep track of all released course materials. Keep in mind that I may shift planned topics to adjust pace as necessary. 

<div class="table-wrapper" markdown="block">

| Week | Date | Topic | Reading | Materials |
| :-: | :- | :- | -: | :- |
| 1 | 9/3 | Introduction  | [Syllabus](https://docs.google.com/document/d/1KVAYYU9B2DLcGQ_XvX9-6RNqVW7b_FI0NXx0UJjzXj4/edit?usp=sharing) | [Survey](https://forms.gle/y7YdmFoi2p2ffc866) [Set-up](https://docs.google.com/document/d/11DtKwHP83sd9BSRk37b5dP8lJ5WRo6Txur-6jF-5plY/edit?usp=sharing) |
| 1 | 9/5 | Language is Hard: Sentence Structure (Syntax)  | Skim [Carnie (2011) Unit 1](https://macalester.on.worldcat.org/oclc/730500579)   | NACLO Problem [1](https://naclo.org/resources/problems/2022/N2022-B.pdf), [2](https://naclo.org/resources/problems/2021/N2021-A.pdf)   |
| 2 | 9/10 | Language is Hard: Word Structure (Morphology)  |    | NACLO Problem [1](https://naclo.org/resources/problems/2021/N2021-G.pdf), [2](https://naclo.org/resources/problems/2023/N2023-M.pdf), [Spaces]({{ site.url }}/notes/spaces.pdf)   |
| 2 | 9/12 | Modeling with Probability  | [Probability Notes]({{ site.url }}/notes/probability_notes.pdf)  |    |
| 3 | 9/17 | N-grams (Maximum Likelihood Estimation)  | Jurafsky & Martin 3.1--3.5   |    |
| 3 | 9/19 | N-grams (Smoothing Techniques)  | Jurafsky & Martin 3.6, 3.8, and Historical Notes  |    |
| 4 | 9/24 | Tokenization | J&M 2.5  |    |
| 4 | 9/26 | CFGs | J&M 18.1--18.6  |    |
| 5 | 10/1 | Parsing  | J&M 18.1--18.6   |    |
| 5 | 10/3 | Probabilistic Parsing 1  | J&M Appendix C   |    |
| 6 | 10/8 | Probabilistic Parsing 2  | J&M 4.1--4.6   |    |
| 6 | 10/10 | Exam Prep  |   | [Practice Exam]({{ site.url }}/notes/practice_exam1.pdf)   | 
| 7 | 10/15 | Exam 1  |   | [Unit 1 Extended Readings](/pages/Unit1Extensions)  |
| 7 | 10/17 | **No Class** (Fall Break)  |   |    |
| 8 | 10/22 | Text Classification (Naive Bayes)  | J&M 4.1--4.6   |    |
| 8 | 10/24 | Text Classification (Logistic Regression) & Evaluation  | J&M 4.7--4.9, 5.1--5.5  |    |
| 9 | 10/29 | Vector Embeddings  | J&M 6  |    |
| 9 | 10/31 | Intro to Deep Learning/Feedforward Networks  | J&M 7.1--7.5   |    |
| 10 | 11/5 | **No Class** (Election Day)  | Complete the "Pytorch Practice" activity on Moodle  |    |
| 10 | 11/7 | Modern NLP Architectures 2 (RNNs/Self-Attention/Transformers)  | J&M 8.1--8.3, 9.1--9.6   |    |
| 11 | 11/12 | Modern NLP Architectures 2 (Self-Attention & Transformers)  | Reread J&M 9.1--9.6   | [Practice Exam]({{ site.url }}/notes/practice_exam2.pdf) |
| 11 | 11/14 | Exam 2 |  |    |

</div> 


### Homeworks

#### Homework 1: N-Gram Language Modeling
**Released: Sep. 17th 5pm** \\
**Due: Oct. 2nd 9pm** \\
Enrolled students should access the Github classroom link through Moodle. 

##### Updates
 - [Advice on doing simple (not stupid!) backoff](/pages/Backoff)

##### Autograding and Revision Policy

Autograding test cases can be found [here](https://github.com/mac-nlp-fa24/hw1-autograding) with a README that explain it's use, as well as where to find the inputs you were tested on along with expected output and detailed logs of how the outputs were computed and the data they were computed from. 

I will re-run the autograder at the end of the semester to determine your implementation score for this assignment for final grades. Consider this a rolling "part 2" of the assignment. The goal is not just to give you a second chance at getting the points, but to encourage you to view multiple stages of writing code, testing code (externally and internally), and revising that code as the standard practice of writing any substantial bit of software. Plus, this is motivation to make sure an assignment you do poorly on is not something to forget about as we move forward. 


#### Homework 2: Text Classification
**Released: Oct 31st 3PM** \\
**Part 1 Due: Nov 7th 9PM** \\
**Due: Nov 19th 9PM** \\
Enrolled students can access the Github classroom link through Moodle.

##### Updates
 - A few bugs in the `data.py` file and a typo in the README are fixed in a pull request sent through Github classroom. 

### Final Project
**Released: Oct 29th 3PM**
**Proposal Due: Nov 21st 9PM**
**Report/Code Due: Dec 15th 9PM**
**Presentations: Dec 16th 1:30--3:30PM**

Guidelines can be accessed by Macalester students [here](https://docs.google.com/document/d/1HFrkZX2SybtMu7fe82mh0f-WNPvFOfx8q_cCpzE69UA/edit?usp=sharing).

##### Updates
 - TBD 
