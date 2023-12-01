# Day 5

## What is a canary deployment strategy?
- is a progressive rollout of an application that splits traffic between an already-deployed version and a new version
- rolling it out to a subset of users before rolling out fully

## What is a canary deployment strategy?
- gives us a chance to partially release our application
- we can ensure the new version of our application is reliable before we can deliver it to all users
- we could deploy the new version of our application to a limited number of pods
- the old version would continue to run, but with more of the traffic being sent to the new pods
