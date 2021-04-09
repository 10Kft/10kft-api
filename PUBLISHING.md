# Publishing 10,000ft API User Guide

## Purpose

This document outlines the process for publishing the 10,000ft API User Guide onto Github Pages. The actual 10,000ft API documentation can be viewed [here CHANGETHIS](http://smartsheet-platform.github.io/odbc-docs). 

## Running the Docs Locally

Follow the steps below if you'd like to run the documentation locally on your machine.

### Prerequisites

 - **Linux or OS X** — Windows also seems to work
 - **Ruby, version 1.9.3 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

 1. Fork this repository on Github.
 2. Clone *your forked repository* (not our original one) to your hard drive.
 3. Navigate to the directory of your local repository.
 4. Install all dependencies: `bundle install`
 5. Start the test server: `bundle exec middleman server`
 6. View the site in a browser:  <http://localhost:4567>

### Learning about Markdown Syntax
 
This documentation is based upon [Slate](https://github.com/tripit/slate/) and uses Slate [markdown syntax](https://github.com/tripit/slate/wiki/Markdown-Syntax).

## Why git version tags?
Git tags are a nice way to keep track of the versions of the documentation. The version of the documentation should match the version of the 10,000ft API that it supports. Example tag name might be `v1.0.1`. This can be added with the following command `git tag v1.0.1`.

## Understanding the publish command
The `rake publish` command bundles all of the resources in the `source/` directory to create static assets in a local directory called `bundle/`. These static assets are then pushed into the `gh-pages` branch. Github pages hosts the contents of the `gh-pages` for public viewing. Only Admins and Owners of the repository have push access into the `gh-pages` repo, so `rake publish` command will fail for anyone else.

`rake publish` script details are located in `Rakefile` and `config.rb`.

## Publishing Process
1. Make sure that the `master` branch has the version of the code you would like to publish. 
2. Tag the branch with a git tag using the command `git tag <TAG_NAME>`.
3. Push the tag to git using the command `git push --tags`.
4. Run the command `rake publish`.
   * You might encounter some deprecated warning messages in the terminal when running `rake publish`, but that is expected and can be ignored.
   * If you run to other errors, try running `bundle exec middleman build` and retrying.
5. In the [Releases CHANGETHIS](https://github.com/smartsheet-platform/odbc-docs/releases) tab of the repository, draft and publish a new release using the tag you created in step 2. 

## Contributing
If you would like to contribute a change to the documentation files, see [Contributing](#CONTRIBUTING).