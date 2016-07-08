---
currentMenu: git
---

# ** Git - Version Control System **

In this section it's described the workflow of the issues.

## 1. [To Do](1todo.html)

### ** When creating a new issue, you MUST abide by these guidelines: **

* when in doubt: create an issue!
* the minimum requirement is a title
* it's acceptable to create the issue in two steps:
 * making a brief description, immediately
 * making a more detailed description, as soon as possible
* introduce the acceptance criteria:
 * objective and formal
 * mandatory, even if vague, for functional questions

## 2. [Ready For Work](2readywork.html)

### ** When dealing with unassigned issues, these are the principles that MUST be followed: **

* manual transitions are done only after it's stablished that the issue has the necessary details needed to its execution
* for issues with funcional impact, the transition needs the approval of the Project Manager (PM)
* either the PM or someone who wants to adress the issue can set the status as "Ready For Work"
* ideally, the estimated amount of time needed to complete the issue should be included


## 3. [Development](3development.html)

### ** When creating/implementing a new feature, you MUST: **

* create the branch from "develop"
* use Git Flow nomenclature (e.g. “feature/”)
* add the project code in upper case (e.g. "IMFQE-XXX")
* review the summary discription manually 

```
<<Git Flow tag>>/<<JIRA Project Code>>-<<JIRA Issue number>>-<<JIRA Issue summary (~30 letters)>>

Ex.: feature/IMFQE-999-docker-support
```

*Tip: You can easily do this, in your web browser, by using [JIRA](https://ubiprism.atlassian.net). Just use the "Create branch" link at the Issue page and follow the steps.*

#### Knowing this, there are some other recommendations that you should follow, regarding issue management:

* the Assignee (the one to whom the issue resolution is assigned) is responsible for the timely progress of the issue
* if relevant, changes to provisioning, migrations, tests or README should be included
* avoid having multiple issues with 'Development' status

### ** On the subject of creating new commits, every commit MUST respect the following structure: **

* a title is required, with a blank line separating the (optional) discription
* titles should be in the format "PROJECTCODE-ISSUENUMBER Some title"
* the description should begin with “If applied, this commit will ... “ or an equivalent expression
* it should not exceed 72 characters

```
<<JIRA Project Code>>-<<JIRA Issue number>> <<JIRA summary (~30 letters)>> <<(optional) commit description>>

Ex.: IMFQE-999 Implemented docker support
```

*Tip: You can just copy the branch name to speedup this process.*

#### Knowing this, there are some other recommendations that you should follow, regarding commit management:

* do some self code-review before opening a new pull-request
* the "resolve" mindset is diferent from “review”
* it can be done online, on Bitbucket, or using “git diff develop”
* every line should be useful to the resolution of the issue at hand
* remove mistakenly introduced code (e.g. spaces)
* avoid 'Since I'm here.." corrections, they should be left to other issues

### ** Concerning acceptance criteria (AC), there are some guidelines that MUST be followed as well, such as: **

* check the AC, item by item; a pull request that doesn't respect the AC is a waste of resources 
* the AC is "law": before you breake it, you have to (and you must) propose a change to it
* revisions to the AC should be made with the approval of the Project Manager
* you can propose changes based on disagreement, unforeseen cases that are not covered or because they can simplify the development process
* modifications to the AC must be done as soon as possible in the development process
* elements out of the AC's scope should be avoided
 
#### Knowing this, there are some other recommendations that you should follow, before opening a new pull request:

* running unit tests is mandatory
* functional tests that, predictably, will fail must be run as well

### ** When your branch is ready, make a pull request using [Bitbucket](https://bitbucket.org/); just go to "Create Pull Request", choose your branch as source and "develop" as destination. **

*Tip: If you are using a command-line interface terminal, at the time you commit, you'll see a link that you can use to get to the pull request creation page.*

## 4. [Code Review](4codereview.html)

### ** When creating a new pull request (PR), you MUST take this principles into account: **

* a description should be made, as it will guide the "reading" of the PR
* if the commit list is empty, the description filling procedure is almost automatic
* resultant dependencies and underlying context needed to the comprehension of the problem should be explicitly mentioned in the PR, eliminating the need to check the issue for additional information

### ** As such, the pull request message MUST have the following signature **

```
<<JIRA Project Code>>-<<JIRA Issue number>>-<<JIRA summary (~30 letters)>> <<(optional) short description>>
```

*Tip: If you follow this principles, the description should be automatically filled for you with a list of the commits made*

### ** Since the Assignee is the author of the pull request (PR), he has the responsibility to guarantee that: **

* the builds pass
* there are no conflicts
* his peers participate and contribute to the code-review
* the PR has, at least, one approve from a coleague
* the PR does not desynchronize too much from develop
* new issues that arise from the debate are opened
* it's clear which sugestions were adressed or which were not
* the issue is marked as reviewed on JIRA

#### Knowing this, there are some other recommendations that you should follow, after opening a new pull request (PR):

* code-review should be done only after the build has passed
* you must reject your own PR if:
 * the changes to be made are conceptually too distinct
 * there are too many changes (>20%)
* avoid multiple push requests
* “code-review” is not a valid description of a commit
* the author of the PR is the one who should mark on Jira that the code-review is finished, making sure that:
    * for every comment made:
        * the proposed solution is accepted by the majority of the participants
        * there were created new issues for questions outside the scope of the PR
        * the scope of the issue was revised (with the Project Manager's approval)

## 5. [Functional Review](5functionalreview.html)

### ** When an issue gets to the stage of funtional review, these are the guidelines that MUST be followed: **

* the assignee must be the Project Manager (PM)
* the PM verifies on QEM the functional impact of QEM
* code-tasks must be used for modifications that are certain to not have any negative functional impact and, with that, the PM can approve the issues swiftly
* it is the PM that approves or merge pull-requests

## 6. [Ready To Deploy](6readydeploy.html)

### ** This is a transitional stage, where: **

* it transitions automaticaly with the merge action, which is one of the reasons why cross-merges are avoided
* [Jenkins](https://jenkins.ubiprism.pt/) does periodic merge tests from develop to master, where it validates that the tests will keep on passing after the merge

## 7. [Deployed](7deployed.html)

### ** This is the final issue estage, where: **

* Jenkins transitions automaticaly to "Deployed"
* as soon as an issue is deployed, it's irreversible; any unaddressed questions or problems introduced must be adressed in other new issues
