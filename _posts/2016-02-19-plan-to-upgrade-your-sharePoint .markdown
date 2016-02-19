---
layout: post
title:  "Plan to Upgrade Your SharePoint "
date:   2016-02-19 00:55:37
categories: Article
---
SharePoint 2016 already in RTM version, we still have to wait a while longer to be tried SharePoint 2016 in Production. Meanwhile, we still can try SharePoint 2016 in development environtment.
Here is a little tips and things to consider when upgrading SharePoint. This article is mostly an experience that we found when upgrading 2010 to 2013, but may still apply when upgrading 2013 to 2016 version.

## Minimize downtime during upgrade

### Read-only databases
You can make database readonly if necessary so that user still can access your site while upgrading SharePoint. A read only database can only be read but no content addition allowed during this phase.

### Parallel database upgrade
You dont need to upgrade your database one by one, you can upgrade more than one database simultaneously. It can reduce overall downtime. Make an experiment first to find optimal number for your system.

## Special cases upgrades
Below are special case that need to address more when upgrading SharePoint.

###Very Large Databases (VLDB)
Larger database means longer downtime. If one database consist of multiple site collection, we can split this database to multiple database. This link has a good info about the process. [https://technet.microsoft.com/en-us/library/cc825328.aspx](https://technet.microsoft.com/en-us/library/cc825328.aspx)

###Forms-based authentication
Before upgrade site content, dont forget to check your custom login form and login process so that it can be applied with new object model.

## Identify Type of Customizations
Now its time to do some research about what customization that have been implemented in our SharePoint farm.
[Test-SPContentDatabase](https://technet.microsoft.com/en-us/library/ff607941.aspx) cmdlet can help you to determine if you missing some sharepoint solution.
If the customiation is not related to SharePoint (eg custom Web services, Windows services, HTTP Module) [Test-SPContentDatabase](https://technet.microsoft.com/en-us/library/ff607941.aspx) will not help you.
You may have to read documentation about your farm, if you dont have any, maybe it is time to documenting it.

After all consideration above are resolved, its time to try it. Just remember that upgrade process are per database content basis. If one of your database content are not ready to upgrade or you are not confident enough to upgrade it, leave it in current version for now while you fix possible error/ missing component in that content Db.

Happy Upgrading...