---
layout: cv
title: The CI/CD Resume Project
---

# The CI/CD Résumé Project

We all know the pain of continuously updating our résumé: applying the ideal format, trimming the fat, keeping track of pertinent details, researching trends, etc. If only there were a way to separate the content from the format, allowing you to distribute the résumé with a variety of formats that pull content from a centralized source with a standardized format!

As an automated focused technologist, this idea led me to a fun realization: a DevOps professional ought to have a deployment pipeline for their résumé!

## Requirements

In order to fulfill my goal, the résumé must adhere to the following:

* Be well documented!
* Produce a web friendly résumé.
* Produce a PDF résumé for distribution.
* Have a single source of truth.
    * This means that the content **must be** separate from the format.
* Have a pipeline to automatically publish the various forms of my resume.
* Support the [Konami code](https://en.wikipedia.org/wiki/Konami_Code).
    * I honestly have no idea why this is a criteria, but as a nerd it just feels right!

## Technologies

The current iteration of this project can be found [here](https://github.com/weshenderson/weshenderson.github.io/tree/main) along with the architectural diagram, pipeline overview, and any supporting documentation. But at a high level this project uses the following technologies:

* Git
    * version control
    * hooks
* GitHub
    * GitHub Actions
    * GitHub Pages
* Bash
    * Automation
* Python
    * Templates
* Docker
    * Runtime environment *(PDF generation)*
* DockerHub
    * Container registry
* HTML/CSS
    * Web content
* Javascript
    * EventListener *(monitor keystrokes)*
    * Ternary operator *(monitor state)*

## Résumés should be Nerdy!

I have interviewed many candidates in my career and I realize that in today's world of ATS and centralized web behemoths this is not the "proper" approach, but I believe that a résumé should have personality and reflect the person and their approach, not just list accomplishments. Because at the end of the day people hire people, not perfectly formatted lists.