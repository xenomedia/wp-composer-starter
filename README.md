[![Build Status](https://jenkins4.xenostaging.com/buildStatus/icon?job=xenomedia/SITENAME/master)](https://jenkins4.xenostaging.com/job/xenomedia/job/SITENAME/job/master/)

# WP Composer Starter for Pantheon
Xeno Media created repository that uses Docker, Composer, WordPress, Jenkins and Pantheon.io hosting.

## Setup
* Download locally
* Copy the composer.json file to your new project's repo
* Update words in the Read me and composer.json files
* Run composer install

## Workflow
Work locally and follow a normal git workflow using a new branch cloned from master.  Merging code into the master branch can only be done with Pull requests.  To test and deploy your changes, follow these steps.

Keep your branch names 11 characters or less.  Pantheon has this limit on multidev environment names.

* Push your branch to Github `git push origin <branch-name>`
  * This will trigger a Job on Jenkins that will build a MulitDev on Pantheon
  * There will be a slack alert in #SITENAME-deploys with a link to the site when it is ready
* Test at http://`<branch-name>`-SITENAME.pantheonsite.io/
* Visit repository on github `hub browse`
* Open a Pull Request `hub pull-request`
  * This will trigger a Job on Jeknins that will sync code back to Pantheon
  * The status can be seen in the PR on GitHub or under the PR numer at https://jenkins4.xenostaging.com/job/xenomedia/job/pan-flow/view/change-requests/
* Once complete, go back to Github and Squash and merge the Pull request
  * This will trigger a Job on Jeknins that will merge the MulitDev to live and flush cache Pantheon
  * There will be a slack alert in #SITENAME-deploys at the start of this process, you will not receive one when it is done.
  * When the merge is complete an alert is sent to #jenkins-ci `ZZ Global Builds » pr_deploy - [buildnumber]-php7a-SITENAME-[branch]-deploy.txt Success after 2 min 6 sec`
* Once the Pull request has been successfully merged and closed, delete the branch from Github and your local
* Test on the live site.

## Referenced Tools
[hub](https://hub.github.com/) is a command-line wrapper for git that makes you better at GitHub.
