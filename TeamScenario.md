# Continuous Delivery for your team

    * Organize into teams of 3-6 people
    * Define roles (you are free to change these at every sprint):
        * Scrum master
        * Product owner (Andrey or Mike)
        * Devops
        * Development
 
We will run 45 minute sprints, 5 minute retrospective, 10 minute weekends

We want to use all the tools and techniques we learned this week.  

    * Test driven development
    * Agile task management with github issues
    * Version control with git
    * Build, test and ship with docker containers
    * Continuous Delivery with Jenkins
    * Extra credit:
      * Implement the praqmatic git flow branching strategy
    
### Sprint contains:

   * Planning: create the github issues to describe the work you will do
   * Working: working on the sprint items
   * Demo: show what was done
   * Retrospective: reflect on how it went and decide on ways to improve

## Iteration 0: The development environment

The end goal for our development process:

 * A build and test environment with docker for developers
 * Have a jenkins server set up to automatically build `master` branches
 * If build and test are ok:
     * Push the image to a docker registry
     * Deploy the web server to production

### Set up a jenkins, docker registry and artifactory server for the team
````
ubuntu@docker:~$ git clone https://github.com/praqma-training/code-infra
````
## Follow the setup instructions
Go here and follow the instructions to make the data directories: https://github.com/praqma-training/code-infra

## Install docker compose
https://docs.docker.com/compose/install/

## Bring the system up
````
ubuntu@docker:~$ cd code-infra/containers
ubuntu@docker:~/code-infra/containers$ docker-compose up
````
Verify that you can reach the server in your web browser.

### Set up the build and test jobs for the application

The starting point for the project is this code [https://github.com/praqma-training/gowebserver](https://github.com/praqma-training/gowebserver).

   1. **Make a fork for your team**. Fork the project in github to make the shared repository for your team.
   2. Enable github issues
   3. Create a kanban board for your project on [waffle.io](waffle.io)
   
## The automation setup

   1. Set up a seed job for the job DSL to make the build and test jobs.
   2. Verify that the jobs are created.
   3. Trigger a build and verify that it is deplyed.

You can [find the instructions for setting this up in the slides](https://docs.google.com/presentation/d/1WPCNSgP0g3Gc0gx1G60D3hl3hdtyclbumsx0Qm10QsY/edit?usp=sharing).

Once you have been through the pipeline, you should find that your application is available at:

   * TESTING: `<YOUR_AWS_SERVER>:8000`
   * PRODUCTION: `<YOUR_AWS_SERVER>:9999`

## The project

We want to build a simple web server in go that fulfils some very important business needs.

We need a `go` web service that when we hit the `/roman/<number>` url it will return the roman numeral representation of it.

````
Given a positive integer number (eg 42) determine
its Roman numeral representation as a String (eg "XLII").

You cannot write numerals like IM for 999.
Wikipedia states "Modern Roman numerals are written by
expressing each digit separately starting with the
leftmost digit and skipping any digit with a value of zero."

Examples:

1 ->    "I" | 10 ->    "X" | 100 ->    "C" | 1000 ->    "M"
2 ->   "II" | 20 ->   "XX" | 200 ->   "CC" | 2000 ->   "MM"
3 ->  "III" | 30 ->  "XXX" | 300 ->  "CCC" | 3000 ->  "MMM"
4 ->   "IV" | 40 ->   "XL" | 400 ->   "CD" | 4000 -> "MMMM"
5 ->    "V" | 50 ->    "L" | 500 ->    "D" |
6 ->   "VI" | 60 ->   "LX" | 600 ->   "DC" |
7 ->  "VII" | 70 ->  "LXX" | 700 ->  "DCC" |
8 -> "VIII" | 80 -> "LXXX" | 800 -> "DCCC" |
9 ->   "IX" | 90 ->   "XC" | 900 ->   "CM" |

1990 -> "MCMXC"  (1000 -> "M"  + 900 -> "CM" + 90 -> "XC")
2008 -> "MMVIII" (2000 -> "MM" + 8 -> "VIII")
  99 -> "XCIX"   (90 -> "XC" + 9 -> "IX")
  47 -> "XLVII"  (40 -> "XL" + 7 -> "VII")

````

## Extra credit!

Add [pre-tested integration](https://wiki.jenkins-ci.org/display/JENKINS/Pretested+Integration+Plugin) for your build.


## Low hanging fruit

Here are some ideas for improvements to the continuous delivery pipeline:

 * Run the unit tests during the build 
 * Add post commit hooks in github to trigger automatically (rather than polling)
