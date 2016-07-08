---
currentMenu: development
---

# ** 3. Development **

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

