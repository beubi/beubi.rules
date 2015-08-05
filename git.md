---
currentMenu: git
---

# Version control system - Git

### When creating implementing a new feature you MUST create a branch with the following signature:

```
<<JIRA Project Code>>-<<JIRA Issue number>>-<<JIRA summary (~30 letters)>>
```  

**You can easily get this by using JIRA: Just use the "Create branch" link at the Issue page.**


### Every commit MUST have the following signature:

```
<<JIRA Project Code>>-<<JIRA Issue number>>-<<JIRA summary (~30 letters)>> <<(optional) commit description>>
```  

**You can just copy the branch name to speedup this process.**

When your branch is ready, make a pull request using bitbucket. Just go to "Create Pull Request" and choose your branch as source and "develop" as destination.

*At the time, when you commit, you'll see a link that you can also use to achieve this.*

### The Pull Request (PR) message MUST have the following signature

```
<<JIRA Project Code>>-<<JIRA Issue number>>-<<JIRA summary (~30 letters)>> <<(optional) short description>>
```  

**If you follow this principles the message should be automatically filled for you**

When you're done you can click at "Create pull request" button.
