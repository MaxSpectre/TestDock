# GitHub Contribution Guidelines

## Branches description

### List of Main Branches
- `development`
- `staging`
- `pre-production`
- `master` (`main`, `production`)

> Deploying should be made only via Merge Request.
> All of these branches have place on server.

#### Development
Branch for developer testing and QA testing. You can make merge request to this branch any release branch even if you don't finish all of the tasks in release. To see how is your feature can work on the server.

#### Staging
Staging branch is a first step before deploying some feature to production.
Make Merge Request to it to start testing by QA 


### List of developed Branches
- `release/<slug_name>`
- `<type>/<ticket_id>-<ticket_slug>`





## Convension of naming

### Ticket branch

    <type>/<ticket_id>-<ticket_slug>

#### type
The first part of the branch. It will fall into one of the following categories:
- `task` - the most common TYPE during developing
- `fix` - if testers find some issue and you should manage it
- `improve` - technical improvement that no need directly for execute some task. More often that we need to merge into all of the current releases.

#### ticket_id
ticket ID is the second part.
For Zentao tickets this is just `id`
For Jira: `<project_code>-<task-id>`

#### ticket_slug
Short text in branch to understand task belonging. Write with using `snake_case`. It can be the title of: **service**, **entity**, **page** or **functionality**. 

> ticket_slug is a manual part so you can ignore it. But try to write the most understandable commits.

#### Example of Naming
```
task/4412-archive
task/4415-space
fix/4516-project_audit
improve/3322-yii_assets
fix/3344
```


### Release branch

    release/<slug_name>

#### slug_name
Slug Name of release can be come short explanation of `release` or it's number if `release` so big and include a lot of features from different sides of project.





## Example of Working Process

1. `master` -> `release-XXXX`
    Create the `release-XXXX` from `master` branch
    
    ```
    git checkout master
    git pull
    git checkout -b <branch-name>
    git push -u origin <branch-name>
    ```

2. `release-XXXX` -> `task/XXXX` 
    To start working with task create branch for this task from `release`, that related to this ticket. Commit you code as mach as you want. 

    > Try to commit often. Then you should merge your changes (all of your commits) back to release branch. Make it only via **Merge Request**. 

    > Don't make a lot changes during developing of one task. Changes shouldn't be more then in 15 files. If you need more changes think about to divide one task to several smaller. There are could be a lot of task in one release*.

3. When you think that `release` is ready, you should merge it into the `staging`. Marging should be only via **Merge Request**. We need `staging` branch to big testing of all functionality that were developed. If we have some trouble we need to fix it into release (maybe to create *fix* branch). Then we need to repeat **Merge proccess** to Staging. 

4. If it is ok you can send `release` to the next step. Create **Merge Request** to the `pre-production` brach. We need `pre-production` to make final test with copy of **production database**. To define all of the hidden issues. If testers find something, make fix in release branch. 

5. When it is ok then we ready to make deployment to production. To do this we need to make merge from `pre-production` branch to `master` branch.





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

