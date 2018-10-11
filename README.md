# CI/CD/CD

[CI vs. CD vs. CD](https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd)

## CONTINUOUS INTEGRATION

Developers practicing **Continuous Integration** merge their changes back to the main branch as often as possible. 

The developer's changes are validated by creating a build and running automated tests against the build. 

By doing so, you avoid the integration hell that usually happens when people wait for release day to merge their changes into the release branch.

Continuous integration puts a great emphasis on **testing automation** to check that the application is not broken whenever new commits are integrated into the main branch.




## CONTINUOUS DELIVERY

**Continuous Delivery** is an extension of continuous integration to make sure that you can release new changes to your customers quickly in a sustainable way. 

This means that on top of having **automated your testing**, you also have **automated your release process** and you can **deploy your application at any point of time** by clicking on a button.

In theory, with continuous delivery, you can decide to release daily, weekly, fortnightly, or whatever suits your business requirements. 

However, if you truly want to get the benefits of continuous delivery, you should deploy to production as early as possible to make sure that you release small batches, that are easy to troubleshoot in case of a problem.



## CONTINIOUS DEPLOYMENT

**Continuous Deployment** goes one step further than *Continuous Delivery*. 

With this practice, every change that passes all stages of your production pipeline is released to your customers. 

**There's no human intervention**, and only a failed test will prevent a new change to be deployed to production.

Continuous deployment is an excellent way to accelerate the feedback loop with your customers and take pressure off the team as there isn't a Release Day anymore. 

Developers can focus on building software, and they see their work go live minutes after they've finished working on it.



































