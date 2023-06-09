---
layout: cv
title: The CI/CD Resume Project
---

# The CI/CD Resume Project

{% include contact.html %}

## Resumes should be Nerdy!

Years ago I stumbled onto Major Hayden's [man-page resume](https://github.com/major/resume/blob/gh-pages/resume.ronn) and have been in love with it ever since. His resume is in the form of a Linux man page; to paraphrase, a nerdy person ought to have a nerdy resume.

This has stuck with me for years and I wanted to have a similarly nerdy resume without just straight-up copying his idea. Recently I had the idea that a DevOps centric person ought to have a DevOps resume, so that's what I set out to do!

In order to fulfil my goal, the resume must adhere to the following:

* Be well documented!
* Produce a web friendly resume.
* Produce a PDF resume for distribution.
* Have a single source of truth.
    * This means that the content **must be** separate from the format.
* Have a pipeline to automatically publish the various forms of my resume.
* Support the [Konami code](https://en.wikipedia.org/wiki/Konami_Code).
  * I honestly have no idea why this is a criteria, it just feels like the right things to do.

## Version 1

My initial thought was to write the resume in markdown, leveraging Jekyll and Pandoc to create the web version and PDF version respectively. This *worked*, however the resulting PDF was not very flattering. I know that Pandoc can produce beautiful documentation, but I was simply not prepared to delve down the rabbit hole that is LateX templates.

I was also able to add Konami support fairly easily by leveraging my Google-fu. I simply made the Javascript open up a new webpage with a different CSS file loaded to give the resume a retro vibe.

In hindsight version 1 was very poorly conceived and I would have benefited from better planning, however it did lay the groundwork and got me excited about the project.

## Version 2

For version 2 I decided to switch to YAML as it offers more flexibility than markdown. This ultimately meant a search for a new templating engine as Jekyll would no longer suffice. As luck would have it I was working on a templating engine for my [main site](https://www.weshenderson.info/) and felt it would serve my purposes nicely; this is sort of a bare-bones project that was really just meant to scratch my programming itch as I have been trying to up my Python game. As for the HTML, I found the [srt-resume](https://sampleresumetemplate.net/) template which I quite liked due to its simplicity and professionalism.

I knew that the pipeline would involve Git hooks as that was something I have been meaning to play with, however I was still unsure how to implement the PDF version of the resume. After playing around with Pandoc I realized that all I really needed was for the CSS to render, something which automatically happened when selecting 'Print to PDF' from your browser. After a bit more Google-fu I learned that Chrome has developer tools that enable the 'Print to PDF' function from a headless instance. All I had to do was tap into that and add it as a pre-commit hook!

```
/usr/bin/google-chrome \
            --headless \
            --disable-gpu \
            --no-pdf-header-footer \
            --no-margins \
            --run-all-compositor-stages-before-draw \
            --print-to-pdf=${PDF} \
            file://${BASE_PATH}/${TMP}
```

*Note: Chrome is [changing](https://developer.chrome.com/articles/new-headless/) the way that headless functions, it will no longer be a standalone browser with a separate codebase. This means that in the near future I will need to revise relevant portions of the hook.*

## Version 3

I did not set out with a version 3 in mind, but after showing my friend the project he introduced me to the [json resume](https://jsonresume.org/)! Conceptually this was very similar to my idea, however it was clear that much more thought went into the schema. Converting also meant that I would be able to incorporate their work, namely their registry and ChatGPT integration. It also meant someone using the jsonresume format could potentially use my templating engine in their own project!

It turns out that changing the underlying schema is not a fun task, but I still believe that it was worth it. I did end up needing a few additional fields for things like Google Analytics, and I found a couple of things lacking in their schema, e.g. it does not have an option to set an employer as current. So in the end my schema is a superset of theirs, but functionally will work on both platforms. 

I decided to stick with YAML for the format as I find it easier to work with; YAML and JSON are easily interchangeable and I simply made my templating engine output a JSON version of the resume as well. With the JSON version in hand I made a GitHub Action to publish it as a Gist so that the JSON registry could pick up the resume.

For version 3 I also decided to fix the Konami resume so that it properly toggled the CSS rather than loading a new page. This is strictly not necessary, but I am a novice web developer wanted to challenge myself. In the end I found a [tutorial](https://www.youtube.com/watch?v=Xk12JtYG8rw&t) by YouTuber Envato Tuts+ that walked me through the process and gave me even more respect for the art of web development!

### Final Workflow

```mermaid!
flowchart LR
    A[Workstation]-->B{{Git Hooks}};
    B-->C((HTML));
    B-->D((PDF));
    B-->E((JSON));
    C-->F[GitHub];
    D-->F[GitHub];
    E-->F[GitHub];
    F-->G{{Actions}};
    G-->H[Pages];
    G-->I[Gist];
    I-->J(Registry);
```

1. A change is made to `configs/resume.yaml`.
2. A [pre-commit hook](https://github.com/weshenderson/weshenderson.github.io/blob/main/.hooks/pre-commit) is executed which generates the following versions of the resume:
   * `resume.json` *(JSON)*
   * `resume.html` *(HTML)*
   * `resume.pdf` *(PDF)*
3. The changes are pushed to GitHub.
4. The following GitHub Actions are ran:
   * [PyLint](https://github.com/weshenderson/weshenderson.github.io/actions/workflows/pylint.yml): Lints my code.
   * [Update Resume Gist](https://github.com/weshenderson/weshenderson.github.io/actions/workflows/resume.yml): Uploads `configs/resume.json` to a public [gist](https://gist.github.com/necrux/47c721cc5ac327c7acc1654fb822005b).
   * [pages-build-deployment](https://github.com/weshenderson/weshenderson.github.io/actions/workflows/pages/pages-build-deployment): Builds and deploys my GitHub Page.
5. The JSON Resume registry is updated with my [new resume](https://registry.jsonresume.org/necrux).
6. My [GitHub Page](https://www.weshenderson.info/) is updated with my new content/resume.

## Conclusion

In the end I am happy with my project and I hope that my resume is sufficiently nerdy. My resume does not present as a nerdy one, but if nothing else it can be an interesting conversation piece and I did learn a lot along the way!