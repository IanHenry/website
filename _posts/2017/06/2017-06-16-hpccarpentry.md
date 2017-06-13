---
layout: post
authors: ["Peter Steinbach"]
title: "HPC in a day?"
date: 2017-06-16
time: "23:00:00"
category: ["Community","Teaching"]
---

__Preface__

In today's scientific landscape, computational methods or scaling thereof onto a set of distributed computers can be at the heart of the race for new insights - if not to be ahead of the academic competition. Learning how to automate tasks from data analysis to preprocessing as taught by the carpentries provides the technical ideas to enter this race in an efficient and intellectually structured way, we hope. But where is the next step? How does someone that finished e.g. the software carpentry boot camp take the next step?

On the ordinary, our just graduated software carpenter is told, that for computational tasks that do not fit on a computer or laptop anymore, the local data center can be approached for time on their compute cluster. Typically, a user account application has to be filed for these High Performance Computing (HPC) facilities and then the project at hand has to be described in a more formal document. This in turn is then reviewed by a scientific advisory board, which eventually grants our carpenter some number of compute hours plus storage space on the cluster. And then? Then either our carpenter is given a link to the wiki of the local cluster and how to use it or there is a short course on the mechanics of the HPC cluster. That's it and good luck.

Clearly, the details of the last paragraph vary from site to site and judging from YouTube, there are a lot of dedicated and highly enthusiastic HPC instructors out there. But based on my personal experience, there is still a large gap from filing an account on the HPC machine to running an analysis or simulation campaign autonomously at scale - simply because HPC clusters are very complicated installations. Moreover, the trainings in HPC jump very quickly to the nuts and bolts of HPC, i.e. the number of cores, size of CPU caches, batch system intrinsic and optimal communication patterns. As many (if not the majority) of HPC users stem from domain sciences and hardly ever received a formal education in (parallel) programming or modern computer design, this situation leaves many users with despair and hopelessness. Many of the latter end up 'copy & paste'ing scripts from wikis or arbitrary places and using them in a mechanical fashion. Simply put: the fun disappears very quickly. With fun lost, creativity will be next which can be detrimental to the scientific race mentioned above. 

__[hpc-novice](https://github.com/swcarpentry/hpc-novice)__

So let's change this! Let's bring fun back to HPC (training). For this purpose, [Christina Koch](christinalk.github.io/) from University of Wisconsin-Madison, [Ashwin Srinath](https://github.com/shwina) from Clemson University and myself (Peter Steinbach from [Scionics Computer Innovation GmbH](www.scionics.de)) started to come about with a [hpc-novice](https://github.com/swcarpentry/hpc-novice) curriculum that is inspired by the software carpentry spirit and pedagogical methods. Although this set of material is still in it's infancy, the idea behind it can be paraphrased by "Bring a graduated software carpenter and his software onto a cluster!". Our efforts to brain storm a possible curriculum to become a new member of the Carpentries are currently fixed in [this document](https://docs.google.com/document/d/1WHPdU7_dlFRytuIJE9I3DJKCd_esiF82ZhTHIIyfRN0/edit?usp=sharing). Feel free to dial over and provide comments.

In an attempt to converge on a curriculum based on user feedback and in the need for local training at our client, the [Max Planck Institute of Molecular Cell Biology and Genetics](www.mpi-cbg.de), I went ahead and came up with an HPC training for one day, which I called [hpc-in-a-day](https://psteinb.github.io/hpc-in-a-day/). I'll dedicate the remainder of this post to giving account on the experiences I made which [people invited me to](https://github.com/swcarpentry/hpc-novice/issues/24#issuecomment-299396469).

hpc-in-a-day was conceived as a local training as our (client) institute is becoming more and more cross-discipline and hence we have mathematicians, physicists, biologists and engineers that all want to use our HPC infrastructure. As we were about to open our new cluster extension, hardware resources were a bit scarce at the time of the workshop. I started to ask around if I could get support from the AWS cloud team through my data carpentry contacts and some vendors that we work closely together with. But not luck. But then, our Lenovo re-seller [pro-com](http://www.pro-com.org/) helped us out and put up a temporary cluster of 8 machines just for our workshop. A big thank you them at this point! 

Before going in, I prepared pre-workshop assessments to infer the expertise level of the learners. I asked them mostly questions on how familiar they are with the terminal and how familiar they were with programming. To give you a feeling of the crowd, 90% of my participants expressed that they use the terminal at least once a day. 45% of all learners mentioned that they would required "google or a colleague of choice" to infer how much disk space they have left on the computer using the terminal. Along the same line of thought, 90% of the participants claimed that they program at least once a day. So I thought well prepared and went ahead composing the material. 

The contents were set up in the following way:

a) 2 sessions about advanced shell methods ([ssh/scp](https://psteinb.github.io/hpc-in-a-day/01-01-taking-the-space-shuttle/) and [file system recap](https://psteinb.github.io/hpc-in-a-day/01-02-filesystems/))
b) 2 sessions on how to submit jobs to the cluster ([scheduler basics](https://psteinb.github.io/hpc-in-a-day/02-01-batch-systems-101/), [submit scripts](https://psteinb.github.io/hpc-in-a-day/02-02-advanced-job-scheduling/))
c) 1 session on using the [shared file system](https://psteinb.github.io/hpc-in-a-day/02-03-shared-filesystem/)
d) 3 sessions on the basics of parallel programming with python (from [serial implementation, to a shared memory parallel one](https://psteinb.github.io/hpc-in-a-day/03-01-parallel-estimate-of-pi/) and a [distributed one](https://psteinb.github.io/hpc-in-a-day/03-02-mpi-for-pi/))
e) 1 session on [using the scheduler for high-throughput computing](https://psteinb.github.io/hpc-in-a-day/03-03-mapreduce-for-pi/)

__What went wrong?__

First of all, I had to learn the hard way that lime survey also records incomplete surveys. It turns out that 2 of my learners didn't complete the survey and those were the ones with rarely any expertise in using the terminal. Me, as the instructor, I need to be more careful with this. Not only did this produce a bi-modal distribution of prior expertise in programming among the participants, but it made structuring the course much more difficult as the majority of learners were able to work with the terminal. 

Second of all, when you are an experienced HPC user and half-time admin, you simply stop seeing the obstacles - many things like file system mechanics are simply done by your fingers and not by your mind anymore. This made my time estimates very inaccurate and tempted me to ditch large parts of some lessons. Judging from this, a 1.5 or even 2 day workshop would be better. A quote from the feedback:

> Course was very intensive (or just too fast) for unexpirienst user. Very fast in the beggining with all the ssh connection, without explanation what is it and how to work with it.

Last but not least, it became apparent in the [feedback round] ([learner 1](https://github.com/psteinb/hpc-in-a-day/issues/9), [learner 2](https://github.com/psteinb/hpc-in-a-day/issues/10), [learner 3](https://github.com/psteinb/hpc-in-a-day/issues/11), [learner 4](https://github.com/psteinb/hpc-in-a-day/issues/12), [learner 5](https://github.com/psteinb/hpc-in-a-day/issues/13), [learner 6](https://github.com/psteinb/hpc-in-a-day/issues/14) and [learner 7](https://github.com/psteinb/hpc-in-a-day/issues/15)) that some of the terms which I used to relate the parallel execution of a program (think "threads on cores") where not mentioned at all in source code. Apparently, this mental mapping was missing and so one learner even said: 

> I’ve also missed examples of how to run programs that already have a --threads option in the cluster. 

even though I covered this type of parallelization in detail. That said I wondered, [if python is really the best language to teach parallel programming?](https://github.com/psteinb/hpc-in-a-day/issues/17)

__What went well?__

In the post-workshop assessment, participants were asked to provide a notion if they would recommend the course to others, where 5 marks very strong agreement and 0 marks no agreement. The feedback form averaged a score of 4.5 out of 5! A quote from the feedback:

> Otherwise, great course. Thanks for having me.

During the course, I saw that many people just assimilated the knowledge that I was trying to convey. Many people immediately asked how to automate job submission, how to profile their Fortran or C++ application, how to automise finding the optimal parameter set for submitting their jobs and much more mostly related to the problems they current have on a day to day basis. I was personally also happy to see that people enjoyed parallel programming as much. I chose the Monte Carlo style estimation of Pi as the underlying algorithmic problem and I had the impression that people could grasp this rather easily - something I was not clear about beforehand.

__Summary__

To put up a carpentry inspired HPC course, some things became evident (again): my hpc-in-a-day curriculum should be split into 2 lessons (`hpc-novice` and `hpc-parallel`) to target people that just want to get their job done on the cluster (`hpc-novice`) and those that need to go further (`hpc-parallel`). A much more clear communication of the expected expertise of the learners is essential. Good teaching of parallel programming and processing can be done before any deep hardware details enter the stage. Working in HPC for years and using these machines should not lead us to believe that we fit to teach it. 

Further, some HPC centers and even one vendors already asked me if and how hpc-in-a-day will live on and if there will be other implementations of it. I personally would love to continue working with Christina and Ashwin as well as any other volunteer out there to do this and potentially bring HPC home into Carpentries. There already was one adaptation of hpc-in-a-day [by Andrea Zonca](https://github.com/swcarpentry/hpc-novice/issues/24#issuecomment-305582614).

