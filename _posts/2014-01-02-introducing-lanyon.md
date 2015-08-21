---
layout: post
title: Front-loading QA in the deploy process
---

Rework is the enemy of productivity. Our highest resource is our developers and the goal is to get as many features deployed into production without calamity as possible. QA is our critical resource because we only have a limited number of deploy candidate environments and it's an opportunity for a lot of stakeholders to get involved.

Currently our developers work on a feature branch and write tests with reasonably good coverage for the feature. Then they make a PR on github and secure 2 code reviewers while our Jenkins CI runs the whole test suite on the branch. Meanwhile our QA team have a large number of integration and functional tests and they are waiting for the CI tests and CR to pass before the feature is merged into a deploy candidate environment, either Release or Hotfix. As soon as the candidate deploy is finished QA starts to run their separate regression test suite and then testing by hand and invite stakeholders to come play. Only the deploy candidate environments have access to external data partners; dev environments mock all data partner calls.


### Several problems here

* QA regression tests are java scripted selenium tests that are hard to run on a laptop dev environment. This means we are always surprised by failures after the code has been peer reviewed.
* QA engineers are inventing tests that duplicate existing unit tests which is a waste of effort.
* Stakeholders and QA spend a lot of time setting up foundation data in order to play with the new feature.
* QA spends most of their time building tests when they could be becoming business knowledge experts.

The big problem is that the dev is left waiting for QA to do their thing and then has to react to any problems which will probably result in a new PR and CR cycle.

### Goal

What we'd really like is to front-load the QA process so that it becomes part of the feature development. We'd like a QA engineer to sit with (perhaps pair with?) the dev during the wrapup phase of development to jointly work on code and feature coverage and design test case fixtures for the deploy candidate environment. We want to convert the integration and functional testing into a capybara framework so that it can also be run easily on the dev's laptop.
