---
layout: cv
title: The CI/CD Resume Project
---

# The CI/CD Résumé Project

We all know the pain of continuously updating our résumé: applying the ideal format, trimming the fat, keeping track of pertinent details, researching trends, etc. If only there were a way to separate the content from the format, allowing you to distribute the résumé with a variety of formats that pull content from a centralized source with a standardized format!

As an automated focused technologist, this idea led me to a fun realization: a DevOps professional ought to have a deployment pipeline for their résumé!

## Requirements

In order to fulfill my goal, the résumé system must adhere to the following:

* Be well documented!
* Multi-target rendering pipeline:
    * Produce a web friendly résumé.
    * Produce a PDF résumé for distribution.
    * Produce a machine friendly `.docx` version for ATS imports.
* Automatically validate generated output and detect regressions.
* Maintain a single source of truth for all résumé content.
* Separate content, presentation, and processing logic.
* Automatically publish the various forms of my résumé.
* Support the [Konami code](https://en.wikipedia.org/wiki/Konami_Code).
    * I honestly have no idea why this is a criteria, but as a nerd it just feels right!

## Implementation Details

The current iteration of this project can be found [here](https://github.com/weshenderson/weshenderson.github.io/tree/main) along with the architectural diagram, pipeline overview, and supporting documentation. Here is a brief overview of the implementation:

* Git
    * version control
    * hooks
    * artifact provenance
* GitHub
    * GitHub Actions
    * GitHub Pages
* Bash
    * Automation
* Python
    * jinga2 (templates)
    * python-docx (machine friendly version for ATS imports)
* Docker
    * Runtime environment (PDF generation)
* HTML/CSS
    * Web presentation
* Javascript
    * EventListener (monitor keystrokes)
    * Ternary operator (track state)

## Résumés should be Nerdy!

I have interviewed many candidates in my career and I realize that in today's world of ATS and centralized web behemoths this is not the "proper" approach, but I believe that a résumé should have personality and reflect the person and their approach, not just list accomplishments. Because at the end of the day people hire people, not perfectly formatted lists.