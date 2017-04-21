# caws
_Caws_ is a web application backend framework built on Crow + AWS SDK that you can pair with, among other things, S3 assets from a domain redirect.  It combines Crow with sqlpp and AWS SDK.  You need to get each of these things to properly use it.

Crow (C++ Web Backend Framework) https://github.com/ipkn/crow
AWS C++ SDK (from Amazon) https://sdk.amazonaws.com/cpp/api/LATEST/index.html
SQLpp (ORM add-on for Crow) https://github.com/rbock/sqlpp11

This means you can host your site primarily on S3 (cheap fast CDN from Amazon), and limit your compute cloud to infrastructure that runs faster than GoLang: C++

A minimal installation includes AWS SDK, Crow and a database driver of your choice such as MySQL.

The approach for developing a _Caws_ site:

* Amzn S3 will hold all of your static pages, Javascript files, fonts, images and static data caches. 
* Static pages, files, fonts and scripts will reference Caws.
* Caws' is the place where your ORM will live, and will respond only in JSON or error codes.

To develop for Caws, we use an insecure starting place.  In the best of environments, you are accessing Caws through a Bastion service which provides granular access tracking and load balancing functionality.  Caws must be extended to run in multiple "shards", which interface with a central hub like AWS IAM (or an RDS) for access control.

Dev Environment

* Caws could access localhost development DB or free tier RDS
* AWS calls from Caws

Live Environment

* Caws accesses private RDS, Aurora or equivalent cluster
* Caws service has a security cert installed, and is using SSL exclusively when hit from outside
* Caws service is managed by a multi-AZ redundant load balanced system

Installation and Getting Started

Linux

_Caws_ requires you to run a Bash-style install script when building.  This will grab the latest copies of the required repos.  You can modify the {./Install} script to suit your setup and situation.  This will deploy your local copy which you will then edit to suit your application needs. You can manually perform the steps in the script if you wish to change anything before building for the first time.

# git clone this repo
# Execute the script to clone the other repos and perform combinatory steps
# Use/modify the ./Recompile script to your liking or roll your own compilation system using whatever make system you'd like.

Windows

This doesn't work on Windows, but you may figure out a way to cross compile it for one of those pseudo-linux platforms, or you can work on it in a VirtualBox or other virtualization technology.

How Caws is implemented

Caws simply sets up the environment, and provides utility classes which you may or may not wish to use, that perform various functions using the AWS SDK.  This is a mere suggestion of what an application should be built like, and you are encouraged to optimize your use of AWS, sqlpp and Crow to best suit your application.

