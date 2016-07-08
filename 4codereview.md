---
currentMenu: codereview
---

# ** 4. Code Review **

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
* “code-review” is not a valid description to a commit
* the author of the PR is the one who should mark on Jira that the code-review is finished, making sure that:
    * for every comment made:
        * the proposed solution is accepted by the majority of the participants
        * there were created new issues for questions outside the scope of the PR
        * the scope of the issue was revised (with the Project Manager's approval)
