# Publishing Resource Management by Smartsheet API User Guide

## Purpose

This document outlines the process for publishing the Resource Management by Smartsheet API User Guide onto Github Pages. The actual Resource Management by Smartsheet API documentation can be viewed [here](https://10kft.github.io/10kft-api/).

## Why git version tags?
Git tags are a nice way to keep track of the versions of the documentation. The version of the documentation should match the version of the Resource Management by Smartsheet API that it supports. Example tag name might be `v1.0.1`. This can be added with the following command `git tag v1.0.1`.

## Understanding the publish command
The `rake publish` command bundles all of the resources in the `source/` directory to create static assets in a local directory called `bundle/`. These static assets are then pushed into the `gh-pages` branch. Github pages hosts the contents of the `gh-pages` for public viewing. Only Admins and Owners of the repository have push access into the `gh-pages` repo, so `rake publish` command will fail for anyone else.

`rake publish` script details are located in `Rakefile` and `config.rb`.

## Publishing Process
1. Make sure that the `master` branch has the version of the code you would like to publish.
2. Run the command `rake publish`.
   * You might encounter some deprecated warning messages in the terminal when running `rake publish`, but that is expected and can be ignored.
   * If you run to other errors, try running `bundle exec middleman build` and retrying.

## Contributing
If you would like to contribute a change to the documentation files, see [Contributing](CONTRIBUTING.md).

## License
Copyright 2021 Smartsheet, Inc.

Licensed under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied. See the License for the specific
language governing permissions and limitations under the
License.
