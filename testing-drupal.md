# Testing A Drupal Distribution

## Challenges Faced

- Inability to test all possible scenarios
- Declining confidence in delivered quality
- Bugs discovered after a new release
- Lack of flexibility in added features
- Accommodating external contributors

## Solutions?

- Switch to major and minor releases
- Test and merge PRs together
- Regular collaboration days with all the teams
- Help external contributors by improving Travis test setup
- Run tests on Enterprise projects for each pull requests

## Project Moss

- Set of tools which help with testing updates
- Test the distro PR for projects to bugs could be spotted before updates were being carried out
- Any fixes ould be placed in special git branch in the project
  - Updating would start from the branch and project specific

1. Create (or update) a PR (speaker uses Primate)
1. Update status to pending
1. Trigger builds for all projects (from Primate to Jenkins)
1. Push code to test branches (from Jenkins to bitbucket)
1. Trigger testing build jobs (from bitbucket to shippable)
1. Post build status (from shippable to primate)
1. UPdate status to success/failed (from primate to project)

## Project speceif fixes

- PRs have their own testing branch for fixes
- Projects have a general fixing branch
