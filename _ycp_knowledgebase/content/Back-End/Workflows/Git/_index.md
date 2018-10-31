---
title: "Git"
---

{{% notice info %}}
**AT ALL COSTS, AVOID PUSHING CODE THAT WILL FAIL TO BUILD!**
{{% /notice %}}

For the Radio Telescope Contracts project, this means that before you push any changes to remote,
you should run the `gradle verify` task; this is essentially an alias for 
`gradle build test jacocoTestCoverageVerification`.

Please note that the CI Server will run this exact gradle task whenever code is pushed, and if your 
build does not pass, neither will the code running on the CI Server, resulting in a failed build.

## Learning Git
If you walked away from CS320 absolutely hating Git, check out [this site](https://learngitbranching.js.org/). It is the best hands-on 
tool I have found to learn about the different git workflows and really teaches you how to harness the power Git offers.

## Git Commit Messages
When writing a commit message, **write in the present tense** (e.g. use "add" and not "added", or
"implement" instead of "implemented"). The first line should be short (~50 characters), concise,
and descriptive (include some context of the module you're working on). Then, if more detail 
is needed to describe the commit contents, an optional extra description should be included on the 
second line.

`git commit -m "Implement Address Entity create command object" -m "that will persist
a new Address record"`

See [What Makes a Good Commit Message?](https://github.com/erlang/otp/wiki/Writing-good-commit-messages) for more information on this

## Branching 
Each **major** feature/project should get it's own branch; typically, these will correlate with 
something marked accordingly on whatever task management software is being used.
If you need to branch off of one of the major branches, that's okay, but it should be 
merged back into a major branch as soon as possible, and **the branch should be removed 
once it is merged!** We don't want 35 stale branches sitting around on our repository and following
this convention will ensure this doesn't happen.

## Temporarily Revert Local Changes 
If you have local changes that you want to roll back, but don't want to lose, and the changes 
are not appropriate for a commit (an example might be some frontend debugging or testing code),
you can use `git stash`. To stash committed or staged changes, simply run `git stash`, or to stash 
*unstaged* changes, run `git stash -u`. For example:
```bash
git stash -u   # repository is now in clean state (mirrors remote); local changes are gone
# do other stuff you wanted to do 
git stash pop  # your changes are back!
```