# GitHub Contribution Guidelines

Working Process -------------------------

All of the work thing should start with creating release branch. Branch it from the *Master* branch.

When you start to work with ticket (that related to this *release*), you should create branch for task from release. Commit you code as mach as you want. Try to commit often. Then you should merge your changes (all of your commits) back to release branch. Make it only via *Merge Request*. 

~Don't make a lot changes during developing of one task. Changes shouldn't be more then in 15 files. If you need more changes think about to divide one task to several smaller. ~

There are could be a lot of task in one *release*.

When you think that release is ready, you should merge it into the *staging*. Marging should be only via Merge Request. We need *staging* branch to big testing of all of  functionality that were developed. If we have some trouble we need to fix it into release (maybe to create *fix* branch) then we need to repeat Merge request to Staging. 

If it is ok you can send *release* to the next step. Create Merge Request to the *pre-production brach*. We need pre-production to make final test with copy of production database. To define all of the hidden issues. If testers find something, make fix in release branch. 

When it is ok then we ready to make deployment to production. To do this we need to make merge from *pre-production* branch to *master* branch.

Convension of naming -------------------------

>>Ticket branch
<type>/<ticket_id>-<ticket_slug>

>>>type
The first part of the branch, the TYPE, will fall into one of the following
categories:
task - the most common TYPE during developing
fix - if testers find some issue and you should manage it
improve - technical improvement that no need directly for execute some task. More often that we need to merge into all of the current releases.

>>>ticket_id
The second part is the ticket ID.
For Zentao tickets there is just *id number*
For Jira: code of the project + task id

>>>ticket_slug
Short text in branch to understand task accessory. Write with using *snake_case*. It can be the title of: service, entity, page or functionality. 

~ticket_slug is a manual part so you can ignore it. But try to write the most understandable commits in this branch.~

Example of Naming: 
task/4412-archive, 
task/4415-space, 
fix/4516-project_audit
improve/3322-yii_assets
fix/3344

Simply create your branch with the name as above, branching from main.
git checkout master
git pull
git checkout -b task/4412-archive
git push -u origin task/4412-archive
_____________________________________

>> Release branch
release/<slug_name>

>>>slug_name
Slug Name of release can be come short explanation of release or it's number if release so big and include a lot of features from different sides of project.


Description of Branches -------------------------

>> List of  main branches

development
staging
pre-production
master (production, main)

(deploying should be made only via Merge Request)



>> List of branches with dynamic parts

release/<slug_name>
<type>/<ticket_id>-<ticket_slug>

>>Development
Branch for developer testing and QA testing. You can make merge request to this branch any release branch even if you don't finish all of the tasks in release. To see how is your feature can work on the server.

>>Staging
Staging branch is a first step before deploying some feature to production.
Make Merge Request to it to start testing by QA 
