---
layout: page
title: Project Final Deliverable
permalink: /assignments/project-deliverable
parent: Assignments
nav_order: 6
---
# Project: Final Deliverable **Due Friday 4/10/2026 6pm (EST)**{: .label .label-red }
The final project deliverable is the implementation, available in github and deployed on Render.com, and the documentation turned in to Canvas. It also includes poster/flier and/or demos. 

## Project Implementation and Documentation
Your final team deliverable will be a "release" of your new feature on GitHub (with tests), and will be accompanied by a demo. You will submit the link of your hosted app on Canvas.

### Contents

Your final team deliverable will include:
* The implementation of your new features, deployed to Render.com or a similar service (e.g. Heroku)
* Automated tests for your new features
* A continuous integration (CI) pipeline
* Project Plan as GitHub Projects
* A report that describes how to use your new feature and what was completed vs proposed
* A poster/flier and/or demo
    
Accompanying the final team deliverable will be an *individual reflection*, which every student must submit on their own which will include your reflections on the evolution of your project concept, on the software engineering processes you used, and on your team's dynamics and collaboration.


### Submission Instructions
**All filed submitted on Canvas must be renamed to include your group number in the file name.** 

#### Code, documentation and Link
 All apps will be deployed on Render.com or a similar service (instructions for CI/CD pipeline setup are provided separately). After you have pushed all of your code (and documentation) to your team's GitHub repository, create [a release](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/managing-releases-in-a-repository) on GitHub, and apply the tag version `final-submission`. After your release is created, you'll find that there is now a `.zip` that can be downloaded from GitHub that contains a snapshot of your entire repository. Download this zip file, unpack it, and follow the instructions that you provided in your README to double-check that the course staff will be able to run your project (this step is handy to make sure that you didn't forget to include some key files in git). If needed, you can delete the release, make some changes, and re-release up until the deadline. **Rename your zip file to include your group number in the file name. Submit this zip file to Canvas** under the assignment "Project: Code Submission" along with **the link of your hosted app** (in comments or a text file). Submit your report separately to Canvas, under the assignment "Project: Report".

#### Continuous Integration Pipeline

In your team's repo on GitHub you must have a CI workflow with the following characteristics: 
- Runs when code is integrated to a mainline branch
- Includes style checks
- Runs all automated unit tests
- Runs e2e tests for the most high value interactions in your application
- Provides quick feedback
- Is repeatable and deterministic
We will provide instructions for CI/CD pipeline setup separately.

#### Project Plan on Issue Tracking Software

Each team is required to use a project management tool (e.g., JIRA, Trello, notion or Github Projects) to track the list of all essential and desirable tasks. In your team's repo on GitHub you must have a link to your tasks and a status update (how much completed).  

#### Project Poster/Flier
Each team **MUST** submit a poster or flier. Your flier will be a single-page 8.5x11 color PDF document, that will include the following aspects:

* Team name
* Team members
* Short description of the project (OK to reuse text from the project plan/report)
* Clickable link to public demo site, clickable link to source repo (OK to make the repo public once the project is submitted, also OK to leave as private)
* Short description of the technology stack and overall design decisions
* Short “what’s next” section describing future work that could build on your project - additional features that you think could be interesting, or ideas for refactoring the code.
* Screenshots of the feature, visually demonstrating the main functionality that you implemented.

Here's an [example flier from Summer 2025]({{ site.baseurl }}{% link Examples/TeamSwanna_Flier.pdf %}) and an example [poster]({{ site.baseurl }}{% link Examples/conversation-areas-poster.pdf %}), but your poster/flier doesn't need to be this highly illustrated. Imagine it as a physical artifact you are giving to the the recruiters or investors as you present your final presentation: your goal is to demonstrate that you have some experience working on some software engineering project that is both technically non-trivial and interesting. There are no specific requirements for font size or amount of text. 

**Each flier/poster must include your group number, names of team members and click-able links to your project repo and hosted app**. Create a PDF of your flier/poster and rename it to include your project name and group number. A physical flier/poster (or printed version) is not needed. **Fliers/posters will be submitted on Canvas**, under the assignment "Project: Poster / Demo".

#### Project Demo/Presentation
In addition to the poster/flier, some sections will have live (in-person) presentations or demos. Details for project demos or presentations will be provided separately by each instructor on the grading rubric page (and may vary from section to section). **Copies of presentations used in demos will be submitted on Canvas**, under the assignment "Project: Poster / Demo" (if required by your instructor).

#### Project Showcase
We will create a project showcase page for this semester (similar to the one from [Spring 2025](https://neu-se.github.io/CS4530-Spring-2025/assignments/project-showcase) semester). You will be asked to indicate your preference (if you don't want your project to be posted there) by completing a survey (a link will be provided in Canvas assignment "Project: Withdraw Permission for Showcase Page"). By default all projects will be posted unless your preference says otherwise. We often direct recruiters to that page. 
 
#### Individual Reflection
Create a PDF of your reflection, and submit it to Canvas, under the assignment "Project: Individual Reflection". 

#### Deadlines
Here are the deadlines for all of the project deliverables:
* Final Implementation (deployed site and code with all tests): Friday April 10th at 6pm EST
* Final Report: Friday April 10th at 6pm EST
* Poster/Flier: The last day of your section's demos/presentations
* Copy of Presentation/Demo: The last day of your section's demos/presentations 
* Individual Reflection: Monday April 20th at 11am EST

**Please note that the filenames for any group submission must include your group number (e.g., project_report_group101_SomeProjectName.pdf).**

## Grading
Details on grading may be found at [Project Grading]({{ site.baseurl }}{% link Assignments/project-grading.md %})