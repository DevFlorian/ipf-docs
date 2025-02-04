# IPF Documentation BETA

This is a GitHub Pages project documenting the [eHealth Integration Platform](https://github.com/oehf/ipf) (IPF).
The documentation is deployed on github at [this](https://oehf.github.io/ipf-docs) location.
The current (official) documentation can still be found [here](https://oehf.github.io/ipf).

The layout is based on the Minimal Mistakes Theme (see description in README-minimal-mistakes.md).

## Why?

The current documentation is difficult and time-consuming to build using Maven's site generator.
The underlying theme is not developed any further and does not work properly with newer versions
of the site plugin.

## Build remotely

There is nothing to be gone. GitHub Pages are automatically rebuilt and redeployed after a commit.
Make sure, however, that `remote_theme` property is enabled the `theme` property is disabled in `_config.yml`.

## Build locally

In order to build and work locally, 

* Follow [these](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) instructions. 
  Hint: install/download the required ruby gems and jekyll plugin without using a proxy!
* For local site generation, comment out the `remote_theme` and enable the `theme` property in `_config.yml`.
* Run `bundle exec jekyll serve`
* The site is served on `http://localhost:4000/ipf-docs`

## TO-DOs

* Javadocs not included yet
* Decide whether other Maven site reports shall be included here (I don't think so)
* Add description here on how/where to add or edit pages
* Add description on how to update the theme
* Links missing, some polishing