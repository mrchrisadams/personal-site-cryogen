{
  :author "mrchrisadams"
  :title "Lessons learned using Github Actions for static site generation with Clojure",
  :date "2020-05-10 13:40:19"
  :draft? true
}

I'm trying to learn clojure in my spare time at the moment, and I've used my personal site as a sample project, because there are a few specific tasks, which I think would be useful to learn to do in the language, namely exporting years of posts from wordpress, and learning to generate static files for hosting somewhere.

This is is the first of a few posts on the subject, and I'll focus on how I set up a way to deploy using Github Actions, as it's new to me, and I can see myself using it a lot in the coming months.

## What is Github Actions?

Github Actions is service that allows you to run programs that do stuff in response to changes being pushed to a repo on github, to allow you to automate common tasks related to working with code.  

You might use it to run different **workflows**, comprised of  specific **jobs** for working on a codebase, from deploying code, to run tests, and other analysis, notifying people of failed jobs and so on. These are typically actions you might rely on a continuous integration service for, and I used it in to:

- run a clojure static site generator to build a website from markdown files
- deploy the changes to a website

If you've ever managed servers, writing these worklows feels a bit like writing playbooks for ansible to automate deployments or manage servers.

Except here, you're not managing individual servers directly. Which I see as a good thing.

## What I like about GH Actions

When working with on larger projects, the fact that continuous integration tracks the state of every build and all the subsequent logs is a really useful.

By default, Github Actions does something similar - generating logs and providing decent visibility into the state of jobs carried out.

This is nice, but you often don't need to retain these logs and build artefacts on smaller projects, and in fact you'd prefer not to have them. Fortunately there's less of a risk of filliing th web with loads of crufty logs from tinkering with personal projects.

> GitHub stores full build logs and artifacts for 90 days.

You can also delete them faster, via the API if need be.

### The default runner machines you are already set up for you.






They're all running hardware of reasonable spec for builds:

- 2-core CPU
- 7 GB of RAM memory
- 14 GB of SSD disk sp

https://help.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners

And they're running on Azure regions:

> Windows and Ubuntu runners are hosted in Azure and have the same IP address ranges as Azure Data centers. Currently, all Windows and Ubuntu GitHub-hosted runners are in the following Azure regions:
>
> - East US (eastus)
> - East US 2 (eastus2)
> - West US 2 (westus2)
> - Central US (centralus)
> - South Central US (southcentralus)


Also, there's also a lot of software already on the runner machines, so you may not need to install anything.

https://github.com/actions/virtual-environments/blob/master/images/linux/Ubuntu1804-README.md


##

### What doesn't work so well

Do not expect ipv6 support

https://github.community/t5/GitHub-Actions/GitHub-Actions-IPv6-Network-Issues/td-p/52085

https://github.com/actions/virtual-environments/issues/668

https://github.com/marketplace/actions/rsyncer-action
https://github.com/actions/virtual-environments/blob/master/images/linux/Ubuntu1804-README.md
https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets

https://help.github.com/en/actions/configuring-and-managing-workflows/authenticating-with-the-github_token

https://github.com/JamesIves/github-pages-deploy-action/issues/285

https://github.com/MichaelCurrin/cheatsheets/blob/master/cheatsheets/ci_cd/github_actions/tokens/README.md