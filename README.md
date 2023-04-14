# teamsykmelding-github-actions-workflows 
This is a repository for GitHub actions workflows for teamsykmelding


## 🚀 Usage
A workflow can be used like this
``` yaml
name: Build & Deploy
on: push

jobs:
  next-app:
    uses: navikt/teamsykmelding-github-actions-workflows/.github/workflows/next-app.yaml@main
    secrets: inherit
    with:
      app: sykmeldinger
      base-path: /syk/sykmeldinger
```

## 👥 Contact

This project is maintained by [navikt/teamsykmelding](CODEOWNERS)

Questions and/or feature requests? 
Please create an [issue](https://github.com/navikt/teamsykmelding-github-actions-workflows/issues)

If you work in [@navikt](https://github.com/navikt) you can reach us at the Slack
channel [#team-sykmelding](https://nav-it.slack.com/archives/CMA3XV997)