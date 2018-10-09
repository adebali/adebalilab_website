---
date: 2018-10-07
description: "Using GitHub Classrom to Teach Computational Biology"
featured_image: ""
tags: ["teaching"]
category: "teaching"
title: "Teaching with Github"
draft: true
author: adebali
---

The current technology allows most of the teaching materials to be shared online. Moreover, it allows you to use a digital repositories to share lecture slides and notes online. Moreover, now it is also possible to create digital assignments. GitHub classroom allows to assign homeworks and dry-laboratory tasks.

I have started teaching a class named `Computational Biology` this semester. This class have regular lecture hours plus 2 hours of lab where students are asked to perform some hands-on activities. These activities are mostly coding.

I wondered if GitHub would be an appropriate place to create an online class reportoir.

## GitHub account

Open a GitHub account if you haven't had yet. The students should have their individual GitHub accounts too.

Add your institutional e-mail address to request unlimited free private repositories that are offered to students, teachers and professors.

Create an organization. Actually you should request private repositories for this organization.

Create two teams in your organization (i) `students` and (ii) `TAs`.


Crate a directory on your local machine; like `ENS210`. The default branch will be named `master`. Consider this branch as a production branch that will display the content to the world. There will however another branch `develop`. The commits of this branch will be pushed to a private repository in your organization. This private repository will be accessed by you as the instructor and TAs.

Create two repositories in your organization. Mine were named `ENS210` and `ENS210_develop`. 

Give read access to `student` team for the main repo `ENS210`. Give read (and write if you like) access to `TAs` for the developing repo `ENS210_develop`.

Create a local `develop` branch with `git checkout develop`. 

Now it is very critical to determine remote urls for these two branches separately. When you are in `master` branch `push` should update the online repository that is open to everyone (`ENS210`). In `develop` branch `push` command should send the commit to the private repo `ENS210` that is available to TAs.

How to do that?

Always work in the `develop` branch. If you need to create and edit files to prepare lectures, lab tasks, assignments and tests, `develop` is the branch that you are interested in. You can share the notes and assignments with your TAs if you push them to the `develop` repo. I also share assignment keys with TAs. 

If the materials in develop are ready for production (this is a full stack term), you can copy your files to the `master` branch.

* First make sure that you are in `master` branch, if not do: `git checkout master`

* Copy the file of interest from `develop` branch to `master` branch with: `git checkout develop myfile.md`

Now you can add the added files, commit them and push them to the 'open' repository. 

```
git add myfile.md
git commit -m "myfile.md added"
git push
```

After this step `file.md` is uploaded to the repository that is accessible by students.

## GitHub Classroom

* Go to [classroom.github.com](classroom.github.com)

* Add a class for your organization.

* Create an assignment by using the 'open' repository like `ENS210` as the starter code. **It is important not to use the `develop` repository here.**

* If you wish, set a deadline.

* Share the link with your students. After they accept the assignment, a repository for each individual and assignment will be created. By the end of the semester in a class of 30 students, total 10 assignments will result in total of 300 unique repositories. It feels like it is against the 'culture' of the repositories, however it is really not. Cosider each repository as an assignment sheet. This way is the easiset to sustain privacy and to provide individual feedback for each assignment.


## Grading

I ask my TA to do the grading for the lab tasks. For each repository he creates a branch named `grading` and submits his grades and edits, which are basically the feedback to the GitHub repo. There is an option to download the all repositories if TA needs to run the scripts locally to chack whether they actually work or not. TA has two options: grading through GitHub by editing the files online or local editing followed by a push. Either way is perfectly fine. 

After TA finishes grading as an instructor I might want to review his grading. If needed I make additional commits to change some grades or to give more feedback to students. After the grading is finalized I create a pull request with some comments. Then the student migth want to accept the request and merge `grading` branch to `master`. If they have an objection, they can easily write their objections as a comment under the pull request page. 




