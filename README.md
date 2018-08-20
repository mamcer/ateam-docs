# ATeam Docs

A [Sphinx](http://www.sphinx-doc.org/en/master/) based documentation site ready to be included in a collaboratively continuous delivery process.

## Description

The goal of this project was to create an Architecture Team area (ATeam, I was a little fan of the '80 TV Serie). Initially focused in the best development practices: Continuous Integration, Continuous Delivery, Continuous Inspection and Unit Testing.  

At that moment using tools like Bamboo for continuous integration and SonarQube for continuous inspection.  

The screenshots basically show my development process of several side-projects.

The repository contains a fully functional documentation site divided in different sections according to the topics above described. The examples are based in .NET. The initial idea was to extend it to another technologies but it never got that maturity level.

The area didn't succeed, at least at my expectation level.

## Install steps

Install, build and test host steps for Ubuntu.

    # install sphinx
    sudo apt-get install python-sphinx
    sudo apt-get install python-pip
    pip install -U sphinx_rtd_theme

    # build documentation site
    sphinx-build -nW -b html docs docs/_build/html
    
    # host the site (quick result review)
    cd docs/_build/html
    python -m SimpleHTTPServer 8080 .

## Screenshots

![screenshot](https://raw.githubusercontent.com/mamcer/ateam-docs/master/doc/screenshot-01.png)

![screenshot](https://raw.githubusercontent.com/mamcer/ateam-docs/master/doc/screenshot-02.png)



A-Team Image from: [fanart](https://fanart.tv/series/77904/the-a-team/)

Favicon from: [freefavicon](https://www.freefavicon.com/freefavicons/objects/iconinfo/a-hand-drawn-heart-152-180829.html)
