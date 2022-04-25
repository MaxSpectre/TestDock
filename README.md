# GitHub Contribution Guidelines

#### Navigate this page
- [General Branches](#general-branches)
  - [Branch: development](#branch-development)
  - [Branch: staging](#branch-staging)
  - [Branch: pre-production](#branch-pre-production)
  - [Branch: master](#branch-master)
- [Dynamic Branches](#dynamic-branches)
  - [Ticket branches](#ticket-branches)
  - [Release branches](#release-branches)
- [Workflow Overview](#workflow-overview)
- [Committing your work](#committing-your-work)
- [Deploying a release branch that has conflicts](#deploying-a-release-branch-that-has-conflicts)





## General Branches
- `development`
- `staging`
- `pre-production`
- `master` (`main`, `production`)

> Merging should be made only via **Merge Request**.
> Merging to this branch leads to deploying.

### Branch: development
Branch for developer testing and QA testing. You can make **Merge request** to this branch from `release` branch even if you don't finish all of the tasks. To see how is your feature can work on the server.

### Branch: staging
Staging branch is a first step before deploying some feature to production.
Make marge to it to start testing by QA.

### Branch: pre-production
Pre-production is second step before daploying. QA engineers should make final test of all features with copy of production database.

### Branch: master
Branch from what we make daployment to production after all testing on previous branches.





## Dynamic Branches

### Ticket branches
Create ticket branch from related `release` 

> it is possible to make ticket branch directly from `master` if we need to make fast feature and deploy it without including in some release.

Ticket branch should have name considering to Name convension

#### Ticket branches Name convension
```
    <type>/<ticket_id>-<ticket_slug>
```

#### Example of Naming
```
task/4412-archive
task/4415-space
fix/4516-project_audit
improve/3322-yii_assets
fix/3344
```

#### type
The first part of the branch. It will fall into one of the following categories:
- `task` - the most common TYPE during developing
- `fix` - if testers find some issue and you should manage it
- `improve` - technical improvement that no need directly for execute some task. More often that we need to merge into all of the current releases.

#### ticket_id
ticket ID is the second part.<br />
For Zentao tickets this is just `id`<br />
For Jira: `<project_code>-<task-id>`

#### ticket_slug
Short text in branch to understand task belonging. Write with using `snake_case`. It can be the title of: **service**, **entity**, **page** or **functionality**. 

> ticket_slug is a manual part so you can ignore it. But try to write the most understandable commits.



### Release branches
Release branch should include a set of tasks and features that we want to prepare for deployment.

Release branch should have name considering to Name convension

#### Release branches Name convension
```
    release/<slug_name>
```

#### slug_name
Slug Name of release can be come short explanation of `release` or it's number if `release` so big and include a lot of features from different sides of project.





## Workflow Overview

1. `master` (create)-> `release-XXXX`

    Create the `release-XXXX` from `master`
    
    ```
    git checkout master
    git pull
    git checkout -b <branch-name>
    git push -u origin <branch-name>
    ```


2. `release-XXXX` (create)-> `task/XXXX`

    To start working with task create branch for this task from `release`, that related to ticket. Commit you code as mach as you want. 
    
    > If we need to make small task faster and don't include it to some release we might not create release for it. Just make `task` branch from master.

    > Try to [commit](#committing-your-work) often. Don't make a lot changes during developing of one task. Changes shouldn't be more then in 15 files. If you need more changes think about to divide one task to several smaller.


3. `task/XXXX` (merge-request)-> `release-XXXX`

    When you finish your work with a task, make **Merge Request** back to **release**.


4. `release-XXXX` (merge-request)-> `staging`

    When you think that `release` is ready prepare **Merge Request** into the `staging`. 
    We need `staging` branch to big testing of all functionality that were developed. If we have some trouble we need to fix it into release (maybe to create *fix* branch). Then we need to repeat **Merge proccess** to `staging`. 


5. `release-XXXX` (merge-request)-> `pre-production`

    Make **Merge Request** from `release` to `pre-production` branch after successfuly testing on staging. 
    We need `pre-production` to make final test with copy of **production database**. To define all of the hidden issues.


6. `pre-production` (merge)-> `master`

    Make **Merge Request** from `pre-production` to `master` branch you sure that pre-production works fine. Production deployment should start only after `master` updating.





## Committing your work
```
    [XXXX] short description of_commit
```

All commits in the branch must start with `ticket_id` on the commit message
e.g. `[4456]` or `[CAM-608]`.

They should then go on to have a short explanation of what has been done in
that commit, e.g:
```
    [4456] Change primary colors from red to green
```

This allows us to easily see which issue each addition came from and what it's
for.

> Remember to commit often, and never to rewrite commit history once you've pushed
> to origin. However, before pushing your commits, you're free to rebase and
> rewrite as you like.


## Deploying a release branch that has conflicts

0. If you're deploying to Production, you just need to merge master into your
   release branch and solve conflicts there. If after doing this and pushing,
   you still have conflicts, please contact a senior developer.
1. For Staging, **create a `conflict-XXXXX` branch from master**, where XXXXX is
   the same ID as the release branch has.
2. **Merge Staging into the conflict branch** using a regular merge, e.g. `git
   merge staging`.
3. **Merge the release into the conflict branch** using a no-fast-forward merge,
   e.g. `git merge --no-ff release-XXXXX`.
4. **Solve the conflicts and merge.** We use a conflict branch for this so that
   all of the Staging history doesn't enter the release branch when it is
   deployed to Production.
5. **Create a pull request to Staging from `conflict-XXXXX`** and then proceed as
   above, making sure the conflict branch is immediately deleted on merge.
   DO NOT MERGE THE CONFLICT BRANCH INTO PRODUCTION OR MASTER.

